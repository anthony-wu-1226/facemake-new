# Project Brief: FacemakeAI v3

## Executive Summary

**Product Concept:** FacemakeAI is an instant professional headshot generator that applies Instagram/NGL-inspired radical simplicity to AI photo generation, allowing users to create high-quality professional photos in under 60 seconds with just 3 taps.

**Primary Problem:** University students and young professionals need professional headshots for LinkedIn, job applications, and professional profiles but face barriers of cost ($200-500 for photo sessions), time (scheduling and travel), and accessibility (finding photographers).

**Target Market:** University students as early adopters (lower objection rates, viral campus potential), expanding to young professionals and remote workers seeking instant, affordable professional photos.

**Key Value Proposition:** Professional headshots in 60 seconds for the price of a coffee, with Instagram-simple UX that removes all complexity from AI photo generation.

## Problem Statement

**Current State & Pain Points:**
Professional headshots remain a significant barrier for students and early-career professionals entering the job market. The traditional photography model requires booking sessions weeks in advance, traveling to studios, spending $200-500 per session, and waiting days for edited results. Students specifically face the triple challenge of limited budgets, unpredictable schedules during exam periods, and lack of professional attire/styling knowledge.

**Impact of the Problem:**
- 87% of recruiters check LinkedIn profiles, yet only 30% of students have professional photos
- Students using professional headshots receive 14x more profile views and 36% more messages
- Average student spends 4-6 hours attempting DIY solutions with poor results
- University career centers report professional photos as #2 barrier to job placement after resume writing

**Why Existing Solutions Fall Short:**
- **Traditional Photography:** Prohibitive cost and time investment for students
- **DIY Attempts:** Inconsistent quality, poor lighting, unprofessional backgrounds
- **Current AI Tools:** Either too complex (Midjourney/Stable Diffusion requiring prompt engineering) or too limited (basic filters that don't achieve professional quality)
- **Competitor Apps:** Focus on avatars/artistic styles rather than genuine professional headshots that pass recruiter scrutiny

**Urgency of Solving Now:**
- Post-pandemic remote work has increased demand for digital professional presence by 400%
- University enrollment at record highs with 20M+ students needing professional photos annually
- AI technology has just reached the quality threshold for professional-grade results
- Previous attempts failed due to poor technical foundation, not market demand - proven need exists

## Proposed Solution

**Core Concept & Approach:**
FacemakeAI v3 implements a "progressive disclosure" architecture where technical complexity scales with feature sophistication, not user interaction. The app presents as dead-simple (3 taps to professional photo) while maintaining a robust, extensible foundation that prevented previous versions from scaling. We're building the technical infrastructure for a full-featured platform but exposing only the Instagram-simple interface initially.

**Key Differentiators:**
- **Radical Simplicity:** 3-tap process (take photo → select style → save) vs competitors' 10+ step workflows
- **Genuine Professional Output:** Google Gemini 2.5 Flash tuned specifically for recruiter-acceptable headshots, not artistic avatars
- **Instant Gratification:** 30-60 second processing vs 24-hour turnaround of manual editing services
- **Progressive Feature Revelation:** Start with 6 options, expand based on user behavior rather than overwhelming initially
- **Campus-Native Distribution:** Built for viral university spread through society partnerships and dorm-room demos

**Why This Solution Will Succeed Where Others Haven't:**
- **Technical Foundation First:** Previous attempts failed from backwards feature building - we're establishing solid architecture before features
- **Validated Simplicity Model:** Instagram/NGL proved users prefer constrained choices over infinite options
- **AI Quality Threshold:** Gemini 2.5 Flash finally delivers professional-grade results that pass LinkedIn/recruiter scrutiny
- **Distribution Advantage:** University partnership strategy provides concentrated early adopter base for rapid iteration
- **Learning from Failure:** Two previous attempts provided clear roadmap of pitfalls to avoid

**High-Level Vision:**
Begin with university students needing LinkedIn headshots, expand to full professional photo suite (conference speakers, dating profiles, visa applications), ultimately become the "Canva for professional photos" - making professional photography accessible to everyone through AI-powered simplicity.

## Target Users

### Primary User Segment: University Students (18-24)

**Demographic/Firmographic Profile:**
- Undergraduate and graduate students across all majors
- Limited disposable income ($50-200/month after essentials)
- High smartphone usage (8+ hours daily), iOS preference (65% iPhone users on campus)
- Active on LinkedIn, Instagram, and university job boards
- Located in university towns with concentrated living (dorms, student housing)

**Current Behaviors and Workflows:**
- Take 20-30 selfies trying to get one "professional enough" photo
- Use ring lights and blank walls in dorm rooms for DIY attempts
- Borrow friends' good cameras without knowing proper settings
- Edit photos through 3-4 different apps trying to achieve professional look
- Postpone LinkedIn profile completion due to lack of professional photo

**Specific Needs and Pain Points:**
- Need professional photos for internship applications (peak seasons: September, January)
- Require quick turnaround during busy exam periods
- Want to look professional but don't own business attire
- Need multiple variations for different platforms (LinkedIn, resume, university portal)
- Concerned about looking "fake" or "overly edited" to recruiters

**Goals They're Trying to Achieve:**
- Stand out in competitive internship/job market (500+ applications per position)
- Build professional online presence before graduation
- Network with alumni and recruiters effectively
- Transition from "student" to "professional" visual identity
- Save money while maintaining professional appearance

### Secondary User Segment: Recent Graduates & Young Professionals (24-32)

**Demographic/Firmographic Profile:**
- Entry to mid-level professionals in first 5 years of career
- Moderate disposable income ($200-500/month)
- Remote or hybrid workers needing digital presence
- Active job seekers or passive candidates open to opportunities
- Urban and suburban locations, often relocated for work

**Current Behaviors and Workflows:**
- Update LinkedIn every 6-12 months for job searches
- Use outdated graduation photos or casual cropped images
- Delay professional photoshoots due to scheduling conflicts
- Try virtual meeting screenshots as makeshift headshots

**Specific Needs and Pain Points:**
- Quick updates for sudden job opportunities
- Consistent professional image across multiple platforms
- Balance between approachable and professional appearance
- Need photos that work across industries (tech casual vs finance formal)

**Goals They're Trying to Achieve:**
- Advance career through strategic job changes
- Build thought leadership and professional brand
- Appear established and competent to senior stakeholders
- Maintain updated presence for unexpected opportunities

## Goals & Success Metrics

### Business Objectives
- **Spark "Aha" Moments:** 10-15 users independently articulate "this would be revolutionary if..." within first week
- **Generate Feature Demand:** Collect 20+ specific feature requests showing users envision the platform's potential
- **Validate Core Promise:** 80% of test users successfully generate a professional headshot they consider "almost good enough"
- **Create Investment Interest:** Document user feedback demonstrating clear path from MVP to revolutionary product
- **Establish Technical Foundation:** Ship working v3 that can actually support the features users request (unlike v1 and v2)

### User Success Metrics
- **Vision Recognition Rate:** 75% of users unprompted mention "this could replace photographers for [specific use case]"
- **Feature Request Quality:** Users suggest specific, implementable features rather than vague improvements
- **Engagement Despite Limitations:** Users complete full flow even with minimal features, showing core value promise
- **Word-of-Mouth Potential:** 50% of users say "I'd tell friends about this once you add [specific feature]"
- **Hope Metric:** Users express excitement about future potential rather than frustration with current limitations

### Key Performance Indicators (KPIs)
- **Feature Request Velocity:** Average 2-3 specific feature suggestions per user
- **Potential Recognition:** Time to first "this could be huge if..." comment < 2 minutes of use
- **Technical Stability:** Zero architecture-breaking issues when adding requested features
- **User Patience Score:** Users willing to wait for features because they see the vision
- **Investment Readiness:** Feedback quality sufficient to include in pitch deck by day 7

### MVP Success Definition
Success is NOT:
- Revenue generation
- Perfect photos
- Complete feature set
- Mass adoption

Success IS:
- Users seeing revolutionary potential
- Specific, actionable feature requests
- Technical foundation that won't break
- Users wanting to stay connected for updates
- Clear product roadmap emerging from user feedback

## MVP Scope

### Core Engine (BUILD FIRST - NO EXCEPTIONS)

**The Image Generation Loop - This is THE MVP:**
1. **Photo Input:** Camera capture or gallery selection
2. **AI Processing:** Pass to Gemini 2.5 Flash with engineered prompts
3. **Result Display:** Show generated image
4. **User Actions:** REGENERATE or SAVE/SHARE

**Critical Parameters:**
- **Angle Options:** Front, Left, Right (3 variations)
- **Background Options:** Professional, Casual (2 variations)
- **Total Combinations:** 6 engineered prompts (3 angles × 2 backgrounds)

### Two Epic Approach

**EPIC 1: Internal User Testing Only (Core Generation Loop)**
- Build the core generation loop (camera/gallery → Gemini API → output)
- Hardcoded API key, insecure, NOT App Store compliant
- Device-in-hand testing with 5-10 trusted users only
- Collect qualitative feedback:
  - Do they get the "aha" moment?
  - Do they tap regenerate/save?
  - Do they call it "good enough" for LinkedIn?
  - What features do they immediately request?
- "The game without menus" - fully functional but not distributable

**EPIC 2: First Public Release (Platform Infrastructure)**
- **Critical Blockers to Address:**
  - Server proxy with JWT auth (no exposed keys, even for TestFlight)
  - Atomic credit decrement (prevent race conditions/unlimited tries)
  - Receipt validation (basic server-side check, not just client flags)
  - File size handling (resize on client or use presigned URLs to avoid Vercel limits)
  - Error states in UI (generation failures, out of credits, API errors)
- **Core Features:**
  - Move API key server-side (Vercel functions)
  - Add auth (Supabase), usage limits, watermarks
  - Implement Apple In-App Purchase ($14.99/month Pro, 3/day Free)
- **Distribution:**
  - App Store/TestFlight compliant
  - 20-50+ user testing group
- "Adding the menus and unlocks" - making it a real product

### Out of Scope for MVP
- Complex UI before engine works
- User accounts before image generation works
- Any feature that doesn't directly support the core loop
- Additional styles/angles beyond the 6 core combinations
- Social features, editing tools, batch processing

### MVP Success Criteria

**Technical Success:**
- Image generation works 100% reliably
- Can switch prompts without breaking
- Can add new prompts without refactoring
- Engine can run independently of UI

**User Success:**
- Users generate professional headshots
- Users hit paywall and consider subscribing
- Users request specific additional features
- Users understand the potential despite limitations

## Post-MVP Vision

### Phase 2 Features (Based on User Feedback)
**Expected Requests We'll Implement:**
- Extended style library (10-20 backgrounds)
- Outfit simulation (business, casual, creative)
- Batch processing (multiple photos at once)
- LinkedIn optimization (specific dimensions/styles)
- History and favorites
- Enhanced angle options (3/4 view, looking away, etc.)

### Long-term Vision (6-12 months)
**Platform Evolution:**
- Full professional photography suite (not just headshots)
- Team/company packages for consistent brand photos
- API for integration with HR/recruiting platforms
- White-label solution for universities
- Photography style marketplace (user-submitted prompts)
- Real-time preview before generation

### Expansion Opportunities
**Market Expansion:**
- Corporate enterprise accounts
- Dating app photo optimization
- Passport/visa photo compliance
- Social media content generation
- Virtual avatar creation for metaverse
- Stock photography disruption

**Technology Expansion:**
- Video headshots for introductions
- AR try-on for different looks
- Voice-synced avatar generation
- Multi-person group photos
- Background environment generation

## Technical Considerations

### Platform Requirements
- **Target Platforms:** iOS (iPhone primary, iPad secondary)
- **Browser/OS Support:** iOS 15+ for native features
- **Performance Requirements:** Image generation < 60 seconds, app response < 100ms

### Technology Preferences

**EPIC 1: Core Image Generation Loop (Client-Only)**
- **Frontend:** Swift/SwiftUI (native iOS, no external dependencies)
- **AI Service:** Google Gemini 2.5 Flash API (direct client calls)
- **Storage:** Local device storage using iOS native APIs
- **No Backend:** Everything runs on device with hardcoded API key

**EPIC 2: Server + Auth + Monetization**
- **Backend:** Vercel serverless functions - ONLY for:
  - Receiving requests (image + style preferences)
  - Checking user credits/plan with Supabase
  - Proxying requests to Gemini API (hiding API key)
  - Returning processed image to client
- **Database:** Supabase - ONLY for:
  - User authentication (email/password)
  - Storing user subscription status (Free/Pro)
  - Tracking daily usage counts (3/day for Free)
- **Payments:** Apple In-App Purchase (required for iOS apps)
- **Watermarking:** Client-side in Swift using Core Graphics
  - Applied locally on device for Free tier users
  - Simple text overlay "FacemakeAI" at bottom corner
  - No external service needed

### Architecture Considerations

**Repository Structure:**
```
facemake-v3/
├── epic1-engine/        # Standalone image gen app
│   ├── src/
│   ├── api-config.js    # Exposed API key (temporary)
│   └── package.json
└── epic2-platform/      # Full platform with server
    ├── client/          # Modified epic1 code
    ├── server/          # Vercel functions
    └── shared/          # Common types/utils
```

**Service Architecture - Progressive Complexity:**

**Stage 1 (Epic 1): Direct Client-to-AI**
```
iPhone → Gemini API (exposed key) → iPhone
```

**Stage 2 (Epic 2): Server Proxy with Auth**
```
1. iPhone → Login (Supabase Auth)
2. iPhone → Vercel Function (image + style + user token)
3. Vercel → Supabase (check credits/plan)
4. Vercel → Gemini API (if credits available)
5. Vercel → iPhone (return generated image)
6. iPhone → Apply watermark locally (if Free tier)
7. iPhone → Save/Share
```

**Technical Flow Details:**
- **Image Handling:** Client resizes to max 2MB before sending (avoid Vercel payload limits)
- **Credit System:** Server-side atomic decrement using Supabase RPC (prevents all race conditions)
- **Auth Check:** Vercel asks Supabase "is this user valid and do they have credits?"
- **Receipt Check:** When user buys Pro, Vercel confirms with Apple before updating Supabase
- **Error Handling:** Show simple messages: "Generation failed", "Out of credits", etc.
- **No Storage:** Images pass through Vercel without saving
- **Watermarking:** Applied on iPhone using Core Graphics (Free tier only)
- **Daily Reset:** Check timestamp - if last use was yesterday, reset to 3 credits

**Integration Requirements:**
- Gemini 2.5 Flash API
- iOS Camera/Photo Library
- iOS Native Share/Save
- (Epic 2 only) Stripe, Auth provider

**Security/Compliance:**
- Epic 1: None (exposed API key is acceptable for testing)
- Epic 2: Secure API keys, user data encryption, GDPR compliance

### Critical Build Principles

1. **Epic 1 MUST work completely standalone** - no server dependencies
2. **Every feature must be testable in isolation** before integration
3. **No complex abstractions** until simple version works
4. **Debugging must be obvious** - know exactly which layer failed
5. **Code must be deletable** - Epic 1 code can be thrown away if needed

## Constraints & Assumptions

### Constraints
- **Budget:** Minimal - using free tiers where possible, ~$100/month for API costs during testing
- **Timeline:** 5-7 days to working Epic 1, additional 3-5 days for Epic 2
- **Resources:** Single developer/small team, no dedicated designer
- **Technical:** Must work on iOS devices, must use Gemini 2.5 Flash (not other AI models)

### Key Assumptions
- **Epic 1 = Complete App:** Users can generate professional headshots without accounts, payments, or server
- **API Key Exposure is Temporary:** Acceptable for 10-15 test users during validation phase
- **Users Will Test Despite Limitations:** Early adopters will overlook rough edges to experience core value
- **Feature Requests > Revenue:** Learning what to build is more valuable than early monetization
- **Progressive Complexity Works:** Adding layers one at a time prevents cascading failures
- **Previous Failures Were Architecture:** Market demand exists, execution was the problem

## Risks & Open Questions

### Key Risks
- **Gemini API Quality:** Generated headshots might not meet professional standards consistently
- **API Cost Explosion:** Exposed key in Epic 1 could be abused (mitigate with quick move to Epic 2)
- **iOS App Store Rejection:** Might require server/auth for App Store submission (Epic 2 dependency)
- **Third Restart Fatigue:** Team morale impact from previous two failures

### Open Questions
- Will Gemini 2.5 Flash maintain consistent quality across different ethnicities/ages?
- How many regeneration attempts before users get acceptable results?
- Can we ship Epic 1 to TestFlight without authentication?
- What's the minimum Epic 2 implementation for App Store approval?
- Should Epic 1 have ANY UI or just be pure function testing?

### Areas Needing Further Research
- Optimal prompt engineering for professional headshots
- Image size/quality settings for best results vs API costs
- TestFlight distribution requirements without backend
- Watermark implementation that doesn't ruin photos
- Usage limiting without user accounts (device-based?)

## Appendices

### Appendix A: Progressive Complexity Build Sequence

#### Build Stage 1: Minimal Loop
```
Open app → Upload photo → Choose styles → Output
```
- Just works, no error handling
- Hardcoded API key
- Single attempt only

#### Build Stage 2: Feedback Loop
```
Open app → Upload photo → Choose styles → Output → Review output → Regenerate if needed
```
- Add regenerate button
- Basic error handling
- Still client-side only

#### Build Stage 3: Server Proxy
```
Open app → Upload photo → Choose styles → Send to server → Output → Review → Regenerate
```
- Move API key server-side
- Add loading states
- Server handles API calls

#### Build Stage 4: Authentication Gate
```
Login → Open app → Upload photo → Choose styles → Server → Output → Review → Regenerate
```
- Add auth wall
- User sessions
- Personal history

#### Build Stage 5: Monetization Layer
```
Login → Open app → Check subscription/credits → Upload photo → Choose styles → Server → Output → Review
```
- Free tier limits (3/day)
- Pro subscription ($14.99)
- Watermark logic

**The Critical Rule:** Each stage must work perfectly before adding the next layer. If Stage 3 breaks, revert to Stage 2 until fixed.

### Appendix B: Research Summary

**Previous Implementation Learnings:**
- V1 failed due to feature-first development causing technical debt spiral
- V2 failed due to broken MVP implementation and developer confusion
- Market research remains valid - demand exists for simplified AI photo generation
- University student early adopter strategy validated through previous attempts

### Appendix C: References

- Original PRD documentation (see olddocs/prd/)
- Previous architecture attempts (see olddocs/architecture/)
- Market research on professional photo demand
- Competitive analysis of existing AI photo tools
- University partnership opportunity research

## Next Steps

### Immediate Actions
1. **Build Epic 1 Core Loop** - Photo input → AI processing → Result display
2. **Test with 5 Internal Users** - Validate the engine works reliably
3. **Deploy to TestFlight** - Get 10-15 external users testing Epic 1
4. **Collect Feature Requests** - Document everything users ask for
5. **Analyze Feedback Patterns** - Identify top 3-5 requested features
6. **Build Epic 2 Infrastructure** - Add server, auth, and payments based on learnings
7. **Re-test with Same Users** - Validate Epic 2 doesn't break Epic 1 functionality

### PM Handoff

This Project Brief provides the full context for FacemakeAI v3, emphasizing a **"game without menus" approach** where Epic 1 delivers complete functionality and Epic 2 adds infrastructure.

**Critical Success Factors:**
- Epic 1 must be a fully functional app (just with exposed API key)
- No complex features until core loop is bulletproof
- Collect feature requests, don't guess what users want
- Two epics only - resist scope creep

**The Mantra:** "If it doesn't generate headshots, it doesn't ship in Epic 1. If it works in Epic 1, Epic 2 must not break it."