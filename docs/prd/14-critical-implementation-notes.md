# 14. Critical Implementation Notes

## 14.1 Subscription Architecture (Epic 2)
**Supabase as Single Source of Truth:**
- Supabase stores and validates all subscription states
- Last verified Apple receipt stored in Supabase
- Client queries Supabase for "Pro" or "Free" status on app launch
- Apple receipt validation only triggered on-demand for:
  - New purchases
  - Renewal checks
  - Dispute resolution
- No client-side subscription checks to prevent spoofing

**Implementation Flow:**
```
1. User purchases → Apple IAP
2. Receipt sent to Vercel → Validates with Apple
3. Vercel updates Supabase → Stores verified state
4. App queries Supabase → Returns subscription status
```

**Rate Limiting Implementation:**
```
Per User: 5 requests/minute, enforced at Vercel
Per IP: 20 requests/hour, enforced at edge
Concurrent: 1 request at a time per user
Gemini timeout: 30 seconds
```

**Watermark Specification:**
```
Text: "Facemake"
Position: Bottom-right corner, 10px padding
Opacity: 30%
Font Size: 3% of image width
Color: White with black outline
Applied: Client-side using Core Graphics
```

## 14.2 UI/UX Decisions
**No Onboarding Flow for MVP:**
- Manual tester onboarding (direct explanation)
- Skip tutorial screens to reduce complexity
- Focus on core 3-tap experience
- Add onboarding only post-MVP based on user feedback

**Mandatory Apple Compliance UI (Epic 2):**
- Subscription terms disclosure before purchase
- "Restore Purchases" button in settings
- Clear pricing display ($14.99/month)
- Cancellation instructions link

## 14.3 Legal Requirements (Epic 2)
**Mandatory for App Store Submission:**
- Terms of Service (link in settings)
- Privacy Policy (link in settings)
- Subscription management options
- Data deletion request mechanism
- First-use consent checkbox

**Implementation:**
- Host legal documents on Vercel
- Simple markdown → HTML rendering
- Links required on:
  - Title screen footer
  - Settings screen
  - Pre-purchase flow
- **Data Retention:** Photos never stored on servers - only processed in temporary memory (<5 seconds)
- **App Store Metadata:** Privacy nutrition labels must reflect data practices above

**Data Storage Clarification:**
```
What We Store (Supabase):
- User email
- Subscription status
- Credit balance
- Generation timestamps
- Apple receipt data

What We DON'T Store:
- Original uploaded photos
- Generated headshots
- Image metadata/EXIF
- Prompt variations
- Gemini API responses
```

**Required Legal Statements:**

Privacy Policy Must Include:
```
"Photos are processed through Google's Gemini 2.5 Flash API but never
stored on our servers. Images exist only in temporary memory during
processing (typically <5 seconds)."
```

Terms of Service Must Include:
```
"You may only upload photos of yourself. Uploading photos of others
without written consent is prohibited and may result in account
termination."
```

**First-Use Consent (Required):**
- Checkbox on first app launch (before any photo capture)
- Text: "I confirm I will only upload my own photos and understand AI processing is involved"
- Store consent timestamp in Supabase
- Cannot proceed without checking

## 14.4 Gemini API Fallback Strategy
**Accepted Risk: No Fallback for MVP**
- Gemini API is single point of failure
- No alternative models or caching
- Explicitly accepted risk for v3 scope

**Error Handling:**
```
if (geminiAPIDown) {
  showMessage("Service temporarily unavailable. Please try again later.")
  logError("API_DOWN_ERROR")
  refundCreditsIfApplicable()
}
```
*Credit Refund Rule: If generation fails for non-user error, auto-refund one credit*

**Rationale:**
- Building redundancy adds unnecessary complexity for MVP
- API reliability sufficient for validation phase
- Focus on core loop validation, not 24/7 uptime
- Users understand MVP limitations
- Aligns with "best effort reliability" NFR

## 14.5 Development Philosophy
**Outcome-Focused Requirements:**
- Specify WHAT, not HOW
- "3-tap flow" not "button at X,Y coordinates"
- "< 60 second generation" not specific loading animations
- Let developers choose implementation details

**Fast Iteration Principles:**
- Requirements define outcomes
- Developers have UI/UX flexibility
- Quick prototyping encouraged
- User feedback drives refinement

---
