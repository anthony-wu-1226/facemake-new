# Supabase Database Setup for FacemakeAI v3

## Critical: Atomic Credit System

Client-side queuing is NOT sufficient. You need server-side atomic operations to prevent:
- Network retries creating duplicate charges
- Multiple devices using same account simultaneously
- Double-taps creating parallel requests
- OS background task replays

## Database Schema

### 1. Users Table
```sql
create table users (
  id uuid primary key default gen_random_uuid(),
  email text unique not null,
  created_at timestamptz default now(),
  subscription_tier text default 'free' check (subscription_tier in ('free', 'pro')),
  apple_receipt_data text
);
```

### 2. Usage Counters Table
```sql
create table usage_counters (
  user_id uuid primary key references users(id) on delete cascade,
  credits int not null default 3,
  last_reset timestamptz default now(),
  updated_at timestamptz default now()
);
```

### 3. Atomic Credit Deduction Function (CRITICAL)
```sql
create or replace function use_credit(p_user_id uuid)
returns table(allowed boolean, remaining int)
language plpgsql
security definer
as $$
declare
  v_remaining int;
  v_tier text;
begin
  -- Get user's subscription tier
  select subscription_tier into v_tier
  from users
  where id = p_user_id;

  -- Pro users always allowed (no credit check)
  if v_tier = 'pro' then
    return query select true, 999; -- unlimited
    return;
  end if;

  -- Lock the user's row to serialize concurrent calls
  update usage_counters
  set
    credits = credits - 1,
    updated_at = now()
  where
    user_id = p_user_id
    and credits > 0
  returning credits into v_remaining;

  if found then
    return query select true, v_remaining;
  else
    -- No credits left (or row missing)
    select credits into v_remaining
    from usage_counters
    where user_id = p_user_id;

    return query select false, coalesce(v_remaining, 0);
  end if;
end $$;
```

### 4. Daily Credit Reset Function
```sql
create or replace function reset_daily_credits()
returns void
language plpgsql
security definer
as $$
begin
  update usage_counters
  set
    credits = 3,
    last_reset = now()
  where
    last_reset < current_date
    and user_id in (
      select id from users where subscription_tier = 'free'
    );
end $$;
```

### 5. Row Level Security (RLS)
```sql
-- Enable RLS
alter table users enable row level security;
alter table usage_counters enable row level security;

-- Users can only read their own data
create policy "Users can view own profile"
  on users for select
  using (auth.uid() = id);

create policy "Users can view own usage"
  on usage_counters for select
  using (auth.uid() = user_id);

-- Only backend (service role) can modify
create policy "Service role can manage users"
  on users for all
  using (auth.role() = 'service_role');

create policy "Service role can manage usage"
  on usage_counters for all
  using (auth.role() = 'service_role');
```

## Vercel Implementation

### API Endpoint: /api/generate-headshot
```javascript
import { createClient } from '@supabase/supabase-js';

const supabase = createClient(
  process.env.SUPABASE_URL,
  process.env.SUPABASE_SERVICE_KEY // service role key for RPC
);

export default async function handler(req, res) {
  const { image, style, angle, userId } = req.body;

  // CRITICAL: Atomic credit check and deduction
  const { data: creditCheck, error } = await supabase
    .rpc('use_credit', { p_user_id: userId });

  if (error || !creditCheck?.[0]?.allowed) {
    return res.status(403).json({
      error: 'No credits remaining',
      remaining: creditCheck?.[0]?.remaining || 0
    });
  }

  try {
    // Now safe to call Gemini API
    const result = await callGeminiAPI(image, style, angle);

    return res.json({
      image: result,
      creditsRemaining: creditCheck[0].remaining
    });

  } catch (error) {
    // Credit was already deducted - you might want to refund it
    // Or just accept the loss (simpler for MVP)
    return res.status(500).json({ error: 'Generation failed' });
  }
}
```

## Testing the Atomic System

### Simulate Race Conditions
```javascript
// Run this from multiple devices/tabs simultaneously
async function testRaceCondition() {
  const promises = [];

  // Fire 10 requests at once
  for (let i = 0; i < 10; i++) {
    promises.push(
      fetch('/api/generate-headshot', {
        method: 'POST',
        body: JSON.stringify({ /* ... */ })
      })
    );
  }

  const results = await Promise.all(promises);

  // Should see only 3 succeed for free user
  // Rest should get "No credits remaining"
}
```

## Cron Job for Daily Reset

### Option 1: Supabase Edge Function (Recommended)
```javascript
// supabase/functions/reset-credits/index.ts
import { serve } from 'https://deno.land/std@0.168.0/http/server.ts'
import { createClient } from 'https://esm.sh/@supabase/supabase-js@2'

serve(async () => {
  const supabase = createClient(
    Deno.env.get('SUPABASE_URL')!,
    Deno.env.get('SUPABASE_SERVICE_ROLE_KEY')!
  );

  await supabase.rpc('reset_daily_credits');

  return new Response('Credits reset', { status: 200 });
});
```

### Option 2: Vercel Cron
```javascript
// vercel.json
{
  "crons": [{
    "path": "/api/cron/reset-credits",
    "schedule": "0 0 * * *" // Daily at midnight
  }]
}
```

## Key Points

1. **Never trust client-side queuing alone** - Always use server-side atomic operations
2. **The RPC function is the gatekeeper** - One SQL transaction prevents all race conditions
3. **Pro users bypass credit checks** - Check subscription tier first
4. **Consider credit refunds** - If Gemini fails after deduction, you might want to refund
5. **Test with parallel requests** - Ensure only allowed credits are consumed

This setup guarantees that even with aggressive parallel requests, users can never exceed their credit limit.