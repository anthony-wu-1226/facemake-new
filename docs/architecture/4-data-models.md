# 4. Data Models

## User Model
```typescript
interface User {
  id: string;                    // UUID from Supabase Auth
  email: string;
  fullName?: string;
  createdAt: Date;
  subscriptionStatus: 'free' | 'pro';
  subscriptionExpiresAt?: Date;
  appleUserId?: string;
  consentAcceptedAt: Date;
}
```

## CreditsBalance Model
```typescript
interface CreditsBalance {
  userId: string;                 // FK to User
  creditsRemaining: number;       // 0-3 for free tier
  lastResetAt: Date;
  updatedAt: Date;
}
```

## GenerationRecord Model
```typescript
interface GenerationRecord {
  id: string;
  userId: string;
  promptStyle: number;           // 1-6
  angleValue: number;            // -1 to 1
  backgroundType: 'professional' | 'casual';
  status: 'pending' | 'success' | 'failed';
  errorCode?: string;
  createdAt: Date;
  processingTimeMs?: number;
}
```
