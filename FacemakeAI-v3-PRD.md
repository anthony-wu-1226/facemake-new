# Facemake v3 Product Requirements Document

## Document Control
- **Product Name:** Facemake v3
- **Version:** 3.0.0
- **Date:** September 2025
- **Author:** Product Management Team
- **Status:** Development Ready
- **Distribution:** Development Team, Stakeholders

---

## 1. Executive Summary

### 1.1 Product Vision
Facemake v3 transforms professional headshot creation through AI-powered instant generation, delivering studio-quality results in 60 seconds via a radically simple 3-tap interface. We're democratizing professional photography by making it accessible, affordable, and instant for university students and young professionals.

### 1.2 Strategic Objectives
- **Primary:** Validate core image generation engine with 10-15 early adopters
- **Secondary:** Collect specific feature requests to guide platform evolution
- **Tertiary:** Establish technical foundation that supports future feature expansion without refactoring

### 1.3 Success Metrics
- 75% of users recognize revolutionary potential within 2 minutes
- 80% successfully generate "almost good enough" professional headshot
- Average 2-3 specific feature requests per user
- Zero architecture-breaking issues when adding requested features

---

## 2. Development Prerequisites

### 2.1 Required Accounts (User Responsibility)
- **Apple Developer Program** - $99/year (required for TestFlight)
- **Google Cloud Account** - With billing enabled (for Gemini API)
- **GitHub Account** - For repository and Vercel deployment
- **Supabase Account** - Free tier sufficient for MVP

### 2.2 Development Environment
- **macOS** - Latest version recommended
- **Xcode 15+** - Required for iOS 17 development
- **Node.js 18+** - For Vercel functions
- **Git** - For version control

### 2.3 Quick Start Guide
1. **Epic 1 (Week 1):** Stories 1.0-1.4 are 100% agent-executable
2. **Story 2.0 (45 min):** User completes all infrastructure setup
3. **Epic 2 (Week 2):** Stories 2.1-2.4 are 100% agent-executable
4. **Result:** TestFlight-ready app in 2 weeks

---

## 3. Problem Statement

### 3.1 Target User Problems

**University Students (Primary Segment)**
- **Cost Barrier:** Professional photos cost $200-500, exceeding monthly budgets
- **Time Constraint:** Cannot schedule sessions during exam periods or irregular schedules
- **Quality Gap:** DIY attempts with dorm lighting produce unprofessional results
- **Career Impact:** 87% of recruiters check LinkedIn, but only 30% of students have professional photos

**Young Professionals (Secondary Segment)**
- **Urgency Issue:** Job opportunities require immediate profile updates
- **Consistency Need:** Multiple platforms require different professional styles
- **Remote Challenge:** No access to local photographers in new cities

### 3.2 Market Evidence
- Students with professional headshots receive 14x more LinkedIn profile views
- 36% increase in recruiter messages with professional photos
- 20M+ university students need professional photos annually
- Post-pandemic remote work increased digital presence demand by 400%

### 3.3 Competitive Analysis

| Competitor | Strengths | Weaknesses | Our Advantage |
|------------|-----------|------------|---------------|
| Traditional Photography | High quality, personalized | $200-500 cost, scheduling required | 60-second generation at coffee price |
| DIY Solutions | Free, immediate | Poor quality, inconsistent | AI-powered professional quality |
| Midjourney/SD | Powerful capabilities | Complex prompts, learning curve | 3-tap simplicity |
| Avatar Apps | Fun, creative | Not professional enough for LinkedIn | Recruiter-acceptable output |

---

## 4. Solution Overview

### 4.1 Core Value Proposition
"Professional headshots in 60 seconds for the price of coffee - Instagram-simple interface with studio-quality AI results"

### 4.2 Key Features (MVP)

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

### 4.3 User Journey (MVP)

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

## 5. Detailed Requirements

### 5.1 Functional Requirements

#### 4.1.1 Image Capture & Input
| Requirement | Priority | Epic |
|-------------|----------|------|
| Camera integration for live capture | P0 | 1 |
| Photo library selection | P0 | 1 |
| Image preview before processing | P0 | 1 |
| Automatic image resizing (max 2MB) | P0 | 2 |

#### 4.1.2 AI Processing
| Requirement | Priority | Epic |
|-------------|----------|------|
| Gemini 2.5 Flash API integration | P0 | 1 |
| 6 pre-engineered prompts | P0 | 1 |
| Server-side API proxy | P0 | 2 |
| Processing time < 60 seconds | P0 | 1 |

#### 4.1.3 User Management
| Requirement | Priority | Epic |
|-------------|----------|------|
| Email/password authentication | P0 | 2 |
| JWT session management | P0 | 2 |
| Credit tracking (3/day free) | P0 | 2 |
| Subscription status management | P0 | 2 |

#### 4.1.4 Monetization
| Requirement | Priority | Epic |
|-------------|----------|------|
| Apple In-App Purchase | P0 | 2 |
| $14.99/month Pro tier | P0 | 2 |
| Receipt validation | P0 | 2 |
| Watermark for free tier ("Facemake" bottom-right, 30% opacity, 3% image width) | P0 | 2 |

### 5.2 Non-Functional Requirements

#### 4.2.1 Performance
- Image generation: < 60 seconds
- App response time: < 100ms
- API timeout: 120 seconds default
- Concurrent user support: 100+

#### 4.2.2 Reliability
- Best effort reliability (downtime risk accepted for MVP)
- Graceful error handling with user-friendly messages
- No automatic retry (complexity avoided for MVP)
- Offline detection and clear messaging
- Minimal telemetry: crash logs + generation duration (no PII)

#### 4.2.3 Security
- No client-side API keys (Epic 2)
- Encrypted user data storage
- Secure JWT authentication
- Apple receipt validation (on-demand only)
- Note: Server-to-server Apple notifications for future versions

#### 4.2.4 Usability
- 3-tap primary flow
- Single-hand operation
- Clear visual feedback
- Intuitive error messages

---

## 6. Technical Architecture

### 6.1 Technology Stack

**Frontend (iOS)**
- Swift/SwiftUI
- Native iOS APIs
- Core Graphics (watermarking)
- AVFoundation (camera)

**Backend (Epic 2)**
- Vercel serverless functions
- Supabase (auth & database)
- Gemini 2.5 Flash API
- Apple StoreKit

### 6.2 System Architecture

**Epic 1: Client-Only Architecture**
```
iOS App → Gemini API (direct, exposed key) → iOS App
```
*Note: Epic 1 builds are internal only; TestFlight requires Epic 2 (no exposed keys)*

**Epic 2: Production Architecture**
```
iOS App → Vercel Functions → Supabase (auth/credits)
                           → Gemini API
                           → Response with image
```

### 6.3 Data Flow

1. **User Authentication** (Epic 2)
   - Login via Supabase Auth
   - JWT token generation
   - Session persistence

2. **Image Processing**
   - Client resizes image (max 2MB)
   - Sends to server with style selection
   - Server validates credits
   - Proxies to Gemini API
   - Returns processed image

3. **Credit Management** (Epic 2)
   - Atomic decrement via Supabase RPC (prevents all race conditions)
   - Daily reset at midnight UTC (or first use after midnight)
   - Real-time balance updates
   - Absolute cap: 3 credits per user per 24 hours

### 6.4 Repository Structure
```
facemake-v3/
├── epic1-engine/        # Standalone generator
│   ├── Facemake.xcodeproj
│   ├── Sources/
│   └── Resources/
└── epic2-platform/      # Full platform
    ├── ios/            # Modified Epic 1
    ├── api/            # Vercel functions
    └── shared/         # Common types
```

---

## 7. User Interface Design

### 7.1 Design Principles
- **Radical Simplicity:** Maximum 3 taps to result
- **Progressive Disclosure:** Complexity scales with features, not interaction
- **Instant Feedback:** Visual confirmation at every step
- **Native iOS Patterns:** Familiar gestures and controls

### 7.2 Core Screens

#### 6.2.1 Title Screen
- App logo and name
- "Get Started" CTA button
- Login option (Epic 2)
- Version number

#### 6.2.2 Capture Screen
- Full-screen camera view
- Gallery selection button
- Front/back camera toggle
- Capture button

#### 6.2.3 Style Selection
- 6 style options (grid layout)
- Visual preview thumbnails
- Simple labels (Professional, Casual)
- Continue button

#### 6.2.4 Result Screen
- Full-screen generated image
- Regenerate button
- Save/Share actions
- Back to start option

### 7.3 Visual Design
- **Color Palette:** Modern, professional blues and grays
- **Typography:** SF Pro (iOS system font)
- **Spacing:** Apple HIG compliant
- **Animations:** Subtle, purposeful transitions

---

## 8. Development Roadmap

### 8.1 Epic 1: Core Engine (Week 1) - 100% Agent Executable

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

### 8.2 Epic 2: Platform Infrastructure (Week 2)

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

### 8.3 Story Execution Notes

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

### 8.4 Story 2.0: User Infrastructure Setup Checklist

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

### 8.5 Post-MVP Roadmap (User-Driven)

**Expected Feature Requests:**
- Extended style library (20+ options)
- Outfit simulation
- Batch processing
- History and favorites
- Team/company packages
- API access

---

## 9. Testing Strategy

### 9.1 Epic 1 Testing
- **Internal Testing:** 5-10 team members
- **Focus:** Core generation reliability
- **Method:** Device-in-hand testing
- **Metrics:** Success rate, generation time

### 9.2 Epic 2 Testing
- **Beta Testing:** 20-50 TestFlight users
- **Focus:** End-to-end user experience
- **Method:** Remote testing with feedback forms
- **Metrics:** Conversion rate, feature requests
- **Restore Purchases Test:** Delete app → reinstall → Restore Purchases returns correct Pro state

### 9.3 Quality Gates

**CEO Testing Checkpoints:**
1. Can generate professional headshot in < 60 seconds?
2. Would pay $14.99/month for unlimited access?
3. What specific features would make this essential?
4. Does the result look LinkedIn-appropriate?

---

## 10. Business Model

### 10.1 Pricing Strategy

**Free Tier:**
- 3 generations per day
- Watermarked images
- Access to all 6 styles
- Basic support

**Pro Tier ($14.99/month):**
- Unlimited generations
- No watermarks
- Priority processing
- Early access to new features

**App Store Configuration:**
- Product ID: `com.facemakeai.pro.monthly`
- Product Name: "Facemake Pro Monthly"
- Price Tier: Tier 15 ($14.99 USD)
- Auto-renewable subscription

### 10.2 Revenue Projections

**Conservative Scenario (Year 1):**
- 10,000 free users
- 5% conversion to Pro
- 500 × $14.99 = $7,495/month

**Growth Scenario (Year 1):**
- 50,000 free users
- 10% conversion to Pro
- 5,000 × $14.99 = $74,950/month

### 10.3 Cost Structure
- Gemini API: ~$0.10 per generation
  - Hard cap: 3 generations/user/day enforced by Supabase
  - Maximum theoretical cost: 10,000 users × 3 × $0.10 = $3,000/day
  - Realistic MVP cost: 50 users × 3 × $0.10 = $15/day
- Vercel hosting: $20/month
- Supabase: $25/month
- Apple fees: 30% of IAP revenue
- **Cost Protection:** Atomic credit decrements prevent race conditions

---

## 11. Risk Management

### 11.1 Technical Risks

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Gemini API quality inconsistency | High | Medium | Multiple prompt variations, user regeneration option |
| API cost explosion | High | Low | Rate limits: 5 req/min per user, 20/hr per IP, 1 concurrent per user |
| iOS App Store rejection | High | Medium | Epic 2 compliance features ready |
| Vercel payload limits | Medium | Medium | Client-side image resizing |

### 11.2 Business Risks

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Low user adoption | High | Medium | University partnership strategy |
| Feature request overload | Medium | High | Strict prioritization framework |
| Competitor rapid response | Medium | Low | Focus on simplicity differentiator |
| Third pivot fatigue | High | Low | Clear success metrics, rapid iteration |

---

## 12. Success Criteria

### 12.1 MVP Success Metrics
- ✅ 75% user "aha moment" within 2 minutes
- ✅ 80% generate acceptable headshot
- ✅ Average 2-3 feature requests per user
- ✅ Zero breaking changes when adding features
- ✅ 50% would recommend "once you add [feature]"

### 12.2 Go/No-Go Decision Framework

**Continue Development If:**
- Users recognize revolutionary potential
- Technical foundation proves stable
- Feature requests are specific and implementable
- Early users express willingness to pay

**Pivot or Stop If:**
- Core generation quality insufficient
- Architecture cannot support requested features
- Users don't see value beyond existing solutions
- Technical costs exceed revenue potential

---

## 12. Stakeholder Communication

### 12.1 Status Reporting
- Daily progress updates during development
- Weekly metrics dashboard post-launch
- Monthly strategic review meetings

### 12.2 Feedback Channels
- In-app feedback button
- TestFlight feedback forms
- Direct email: feedback@facemakeai.com
- GitHub issues for technical feedback

---

## 13. Appendices

### 13.1 Prompt Engineering Templates (6 Core Styles)

**Style 1: Professional Front-Facing**
```
Generate a professional headshot of the person in this image:
- Direct front-facing angle, shoulders square to camera
- Modern office background with soft bokeh
- Business professional attire (suit/blazer suggested)
- Soft studio lighting from 45-degree angle
- Confident smile, direct eye contact
- LinkedIn-appropriate, corporate styling
- Clean, polished appearance
```

**Style 2: Professional Side-Angle**
```
Generate a professional headshot of the person in this image:
- 45-degree side angle, face turned toward camera
- Neutral gray or white backdrop
- Business professional attire
- Dramatic side lighting for depth
- Thoughtful, focused expression
- Executive portrait style
- Sharp, high-contrast details
```

**Style 3: Professional Three-Quarter**
```
Generate a professional headshot of the person in this image:
- Three-quarter view angle (between front and profile)
- Blurred conference room or bookshelf background
- Business casual attire (dress shirt/blouse)
- Natural window lighting effect
- Approachable, warm expression
- Modern corporate headshot style
- Balanced, symmetrical composition
```

**Style 4: Casual Front-Facing**
```
Generate a professional headshot of the person in this image:
- Direct front-facing angle, relaxed posture
- Outdoor or coffee shop background, softly blurred
- Smart casual attire (polo, casual button-up)
- Natural, warm lighting
- Genuine, friendly smile
- Approachable startup/tech style
- Vibrant, engaging appearance
```

**Style 5: Casual Side-Angle**
```
Generate a professional headshot of the person in this image:
- 45-degree casual angle, natural head turn
- Urban or brick wall background
- Casual professional attire (sweater, casual shirt)
- Golden hour lighting effect
- Relaxed, confident expression
- Creative industry style
- Artistic, contemporary feel
```

**Style 6: Casual Three-Quarter**
```
Generate a professional headshot of the person in this image:
- Three-quarter casual angle
- Park or natural environment background, bokeh effect
- Weekend professional attire (smart casual)
- Soft, diffused natural lighting
- Easy-going, authentic expression
- Lifestyle professional style
- Warm, inviting composition
```

**Prompt Testing Requirements:**
- Each prompt must be tested with 20+ diverse faces
- Document success rate per demographic
- Flag any consistent failures for immediate dev review
- A/B test variations if quality drops below 80% satisfaction

### 13.2 Error Messages

| Error Condition | User Message | Technical Log | Action |
|-----------------|--------------|---------------|---------|
| API timeout | "Taking a bit longer than usual..." | GEMINI_TIMEOUT_ERROR | Auto-refund credit |
| No credits | "You've used today's free photos. Upgrade to Pro for unlimited!" | CREDITS_EXHAUSTED | Show upgrade button |
| Network error | "Check your connection and try again" | NETWORK_UNAVAILABLE | Show retry button |
| Generation failed | "Let's try that again" | GENERATION_FAILED | Auto-refund credit |
| Image too large | "Photo too large. We'll resize it for you." | IMAGE_RESIZE_REQUIRED | Auto-resize and proceed |
| Invalid format | "Please use JPEG, PNG, or HEIC format" | INVALID_IMAGE_FORMAT | Return to camera |
| Multiple faces | "Please use a photo with only one person" | MULTIPLE_FACES_DETECTED | Return to camera |
| No face detected | "Couldn't find a face. Try a different photo" | NO_FACE_DETECTED | Return to camera |
| Inappropriate content | "This image cannot be processed" | CONTENT_VIOLATION | Return to camera |
| Server overloaded | "High demand right now. Please try again in a moment" | SERVER_OVERLOAD | Show retry in 30s |
| Prompt failure | "Technical issue detected. Our team has been notified" | PROMPT_GENERATION_ERROR | Auto-refund, flag for dev review |

### 13.3 Glossary
- **Epic:** Major development milestone
- **MVP:** Minimum Viable Product
- **IAP:** In-App Purchase
- **JWT:** JSON Web Token
- **P0:** Priority 0 (critical requirement)

---

## Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| Product Manager | John (PM Agent) | Approved | 2025-09-14 |
| Tech Lead | TBD | Pending | |
| CEO | Anthony Wu | Pending | |
| Lead Developer | TBD | Pending | |

---

## 14. Critical Implementation Notes

### 14.1 Subscription Architecture (Epic 2)
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

### 14.2 UI/UX Decisions
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

### 14.3 Legal Requirements (Epic 2)
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

### 14.4 Gemini API Fallback Strategy
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

### 14.5 Development Philosophy
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

## 15. Context7 Architecture Alignment

### API Design Standards
**Endpoint Structure (Epic 2):**
```
POST /api/generate
  Headers: Authorization: Bearer [JWT]
  Body: {
    image: base64_string,
    style: 1-6 (style number),
    userId: string
  }
  Response: {
    success: boolean,
    imageUrl?: string,
    error?: string,
    creditsRemaining?: number
  }
```

**Error Response Format:**
```json
{
  "success": false,
  "error": {
    "code": "CREDITS_EXHAUSTED",
    "message": "You've used today's free photos",
    "userAction": "upgrade"
  }
}
```

### Security Best Practices
- JWT tokens expire after 24 hours
- Refresh tokens stored securely in Keychain (iOS)
- API keys never exposed in client code
- All API calls over HTTPS
- Input validation on both client and server

### Performance Optimization
- Image compression before upload (max 2MB)
- CDN for static assets (legal docs)
- Lazy loading for non-critical features
- Response caching for subscription status (5 min TTL)

### Monitoring & Observability
```
Required Metrics:
- API response time (p50, p95, p99)
- Generation success rate
- Credit usage patterns
- Error frequency by type
- User funnel conversion
```

---

## 16. Quick Reference Checklist

### Epic 1 Must-Haves
- [ ] Camera/gallery input working
- [ ] 6 hardcoded prompts functional
- [ ] Gemini API generating images
- [ ] Save/share functionality
- [ ] Basic error messages

### Epic 2 Must-Haves
- [ ] Supabase auth working
- [ ] Server-side API proxy deployed
- [ ] Credit system (3/day free)
- [ ] Apple IAP integrated
- [ ] Watermarking for free tier
- [ ] Terms of Service linked
- [ ] Privacy Policy linked
- [ ] Restore Purchases button
- [ ] Subscription state in Supabase
- [ ] First-use consent checkbox implemented
- [ ] Consent timestamp stored in Supabase

### NOT in MVP
- ❌ Onboarding screens
- ❌ Multiple AI model fallbacks
- ❌ Offline mode
- ❌ User history
- ❌ Social features
- ❌ Advanced editing tools

---

## 18. Implementation Readiness Summary

### Ready to Start ✅

**This PRD is now READY FOR IMPLEMENTATION with:**

1. **Clear Two-Epic Structure**
   - Epic 1: 100% agent-executable (Stories 1.0-1.4)
   - Epic 2: One user setup story + 4 agent stories

2. **Consolidated User Tasks**
   - ALL manual setup in single Story 2.0 (45 minutes)
   - Clear checklist with exact steps
   - Credentials handoff via env file

3. **Continuous Project Integrity**
   - Story 1.0 creates foundation with branding
   - Every story maintains Xcode project
   - No regression risk

4. **Defined Success Criteria**
   - < 60 second generation
   - 6 distinct styles
   - TestFlight ready in 2 weeks

### Start Command for Development Team

```bash
# Week 1 - Epic 1
Execute Story 1.0: Create iOS project with branding
Execute Stories 1.1-1.4: Build core generation loop

# Week 2 - Epic 2
User: Complete Story 2.0 infrastructure setup (45 min)
Execute Stories 2.1-2.4: Add platform features

# Result
TestFlight submission ready
```

**Project Status: APPROVED FOR DEVELOPMENT**

---

*End of Document - Version 3.1.0 (Implementation Ready)*