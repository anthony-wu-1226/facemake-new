# 4. Solution Overview

## 4.1 Core Value Proposition
"Professional headshots in 60 seconds for the price of coffee - Instagram-simple interface with studio-quality AI results"

## 4.2 Key Features (MVP)

**Epic 1 — Core Generation Flow (Proof of Loop)**

*Focus:* User can choose/upload a photo, pick a style, send it to Gemini, and get an image back.

**User Flow:**
1. **Upload/Take Photo** → User captures selfie or selects from gallery
2. **Select Style** → User adjusts angle slider and chooses professional/casual background
3. **Processing** → User sees loading animation while Gemini generates (< 60s)
4. **"Good?" Feedback** → User evaluates result and can regenerate with same/different style
5. **Save/Share** → User saves to camera roll or shares to LinkedIn/social

**Technical Note:** API key stored client-side for internal testing phase only

**Definition of Done:**
- ✓ End-to-end generation loop works in < 60 seconds
- ✓ Regenerate feedback loop allows infinite attempts
- ✓ Image saves to camera roll with proper permissions
- ✓ All 6 style combinations produce distinct results

---

**Epic 2 — Platform Infrastructure (TestFlight-Ready)**

*Focus:* Wrap the loop with accounts, credits, monetization, and compliance.

**User Flow:**
1. **Main Menu + Login/Signup** → User creates account via email or Apple Sign In
2. **Credits Tracking** → User sees remaining credits (3/day free vs. unlimited Pro)
3. **Generation with Limits** → Free users consume credits; Pro users have unlimited
4. **Settings & Upgrade** → User can upgrade to Pro, restore purchases, manage account
5. **Legal & Consent** → User accepts terms, sees privacy policy, consents to AI usage

**Technical Note:** Supabase Auth + Credits RPC, Apple IAP integration, client-side watermark for free tier

**Definition of Done:**
- ✓ User can sign up and maintain persistent sessions
- ✓ Credits correctly decrement (atomic operations, no race conditions)
- ✓ Free vs. Pro differentiation works (watermark, limits)
- ✓ Apple IAP purchase and restore flows functional
- ✓ Passes App Store review requirements (legal links, restore button, clear pricing)

## 4.3 User Journey (MVP)

**Epic 1 Journey (Core Loop):**
```
Open App → Capture/Upload → Adjust Style Slider → Generate
              ↓                                        ↓
         Save/Share ← Satisfied? ← View Result
                           ↓ No
                      Regenerate
```

**Epic 2 Journey (Full Platform):**
```
Open App → Login/Signup → Check Credits → Capture/Upload
                ↓                              ↓
    Settings ← Main Menu              Adjust Style → Generate
        ↓                                     ↓
    Upgrade to Pro              View Result (watermarked if free)
                                      ↓
                              Save/Share or Regenerate
```

---
