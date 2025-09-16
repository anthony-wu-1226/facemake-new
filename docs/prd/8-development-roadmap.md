# 8. Development Roadmap

## 8.1 Epic 1: Core Engine (Week 1) - 100% Agent Executable

**Objective:** Validate core generation loop with internal testing

**Stories:**
1. **Story 1.0:** Initial iOS Project Creation
   - Create Xcode project with SwiftUI template
   - Configure Info.plist for camera/gallery permissions
   - Add app icon and launch screen
   - Set app display name to "Facemake"
   - Configure bundle identifier (com.facemakeai)
   - Set up project structure and dependencies
   - Initialize git repository

2. **Story 1.1:** Camera/Gallery Integration
   - Implement camera capture functionality
   - Add photo library selection
   - Create image preview interface

3. **Story 1.2:** Style Selection UI
   - Build angle slider (-1 to 1)
   - Add professional/casual toggle
   - Implement style preview

4. **Story 1.3:** Gemini Integration (Hardcoded Key)
   - Integrate Gemini 2.5 Flash API
   - Build 6 prompt combinations
   - Add loading states

5. **Story 1.4:** Save/Share Functionality
   - Implement save to camera roll
   - Add share sheet integration
   - Complete regeneration loop

**Success Criteria:**
- Generates professional headshots in < 60s
- All 6 style combinations work
- 5-10 internal users provide feedback

## 8.2 Epic 2: Platform Infrastructure (Week 2)

**Objective:** Production-ready app with auth and monetization

**Stories:**
1. **Story 2.0:** Complete Infrastructure Setup (USER ONLY - 45 minutes)**
   - See Section 7.4 for detailed user setup checklist
   - All manual account creation and configuration
   - Delivers credentials.env file to agent

2. **Story 2.1:** Authentication Implementation (Agent)
   - Integrate Supabase Auth SDK
   - Build login/signup screens
   - Implement session management

3. **Story 2.2:** Credit System (Agent)
   - Connect to Supabase RPC functions
   - Display credit balance
   - Implement daily reset logic

4. **Story 2.3:** IAP Integration (Agent)
   - Configure StoreKit 2
   - Add purchase flow
   - Implement restore purchases

5. **Story 2.4:** Watermarking & Polish (Agent)
   - Add watermark to free tier images
   - Complete error states
   - Final UI polish

**Success Criteria:**
- TestFlight deployment successful
- All App Store requirements met
- Payment processing works
- No exposed API keys

## 8.3 Story Execution Notes

**Critical for All Agent Stories:**
```yaml
Pre-Implementation:
  - Open existing Xcode project
  - Pull latest changes
  - Verify build succeeds

Implementation:
  - [Story-specific tasks]
  - Add new files to Xcode project
  - Update project.pbxproj if needed
  - Test in simulator

Post-Implementation:
  - Commit all changes including .xcodeproj
  - Verify build still succeeds
  - Document any new capabilities added
```

## 8.4 Story 2.0: User Infrastructure Setup Checklist

**Prerequisites:**
- Apple ID with payment method
- GitHub account
- Google account with billing enabled
- ~45 minutes uninterrupted time

**Step 1: Apple Developer (10 min)**
```
1. Join Apple Developer Program ($99/year)
2. Create App ID: com.facemakeai
3. In App Store Connect:
   - Create app "Facemake"
   - Add IAP: com.facemakeai.pro ($14.99/mo)
4. Save Team ID
```

**Step 2: Google Gemini API (5 min)**
```
1. Go to console.cloud.google.com
2. Create project "facemakeai-v3"
3. Enable "Generative Language API"
4. Create API key (restrict to Gemini 2.5 Flash)
5. Save API key
```

**Step 3: Supabase Setup (10 min)**
```sql
1. Create project at supabase.com
2. Run in SQL Editor:

CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE credits_balance (
  user_id UUID PRIMARY KEY REFERENCES users(id),
  credits_remaining INT DEFAULT 3,
  last_reset_at TIMESTAMP DEFAULT NOW(),
  is_pro BOOLEAN DEFAULT FALSE
);

CREATE OR REPLACE FUNCTION decrement_credits(uid UUID)
RETURNS INTEGER AS $$
DECLARE
  remaining INT;
BEGIN
  UPDATE credits_balance
  SET credits_remaining = credits_remaining - 1
  WHERE user_id = uid
    AND credits_remaining > 0
    AND is_pro = FALSE
  RETURNING credits_remaining INTO remaining;

  RETURN COALESCE(remaining, 0);
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

3. Save Project URL, Anon Key, Service Key
```

**Step 4: Vercel Setup (5 min)**
```
1. Sign up at vercel.com
2. Import repository (after Story 1.0)
3. Add environment variables:
   - SUPABASE_URL
   - SUPABASE_ANON_KEY
   - SUPABASE_SERVICE_KEY
   - GEMINI_API_KEY
4. Save deployment URL
```

**Step 5: Create credentials.env**
```env
# Apple
APPLE_TEAM_ID=YOUR_TEAM_ID
BUNDLE_ID=com.facemakeai

# Gemini
GEMINI_API_KEY=YOUR_API_KEY

# Supabase
SUPABASE_URL=https://xxx.supabase.co
SUPABASE_ANON_KEY=YOUR_ANON_KEY
SUPABASE_SERVICE_KEY=YOUR_SERVICE_KEY

# Vercel
VERCEL_URL=https://facemakeai.vercel.app

# IAP
IAP_PRODUCT_ID=com.facemakeai.pro
```

**Step 6: Xcode Signing (5 min)**
```
1. Open Xcode project (from Story 1.0)
2. Select project > Signing & Capabilities
3. Set Team and Bundle ID
4. Add capabilities:
   - Camera
   - Photo Library
   - In-App Purchase
```

## 8.5 Post-MVP Roadmap (User-Driven)

**Expected Feature Requests:**
- Extended style library (20+ options)
- Outfit simulation
- Batch processing
- History and favorites
- Team/company packages
- API access

---
