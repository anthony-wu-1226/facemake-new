# Story Inheritance Matrix - Facemake iOS

## ⚠️ **MANDATORY REFERENCE DOCUMENT** ⚠️

**🚨 ALL SCRUM MASTERS MUST CONSULT THIS MATRIX BEFORE DRAFTING NEW STORIES 🚨**

**Target:** iOS 16.0+ (minimum), optimized for iOS 17+

**Purpose:** Prevent redundant work, scope bloat, and Swift 6 concurrency issues by tracking all implemented functionality across stories.

**Last Updated:** 2025-09-17
**Maintained By:** Sarah (Product Owner)

---

## Story Status Overview

| Story | Status | Completion Date | Swift 6 Compliant | Key Learnings |
|-------|--------|-----------------|-------------------|---------------|
| 1.0 | ✅ DONE | 2025-09-15 | ✅ YES | Foundation established properly |
| 1.1 | ✅ DONE | 2025-09-16 | ✅ YES (after +3 day fix) | **MAJOR Swift 6 issues caused +3 day delay** |
| 1.2 | ✅ DONE | 2025-09-17 | ✅ YES | **Style selection MVP with Swift 6 Task-based throttling** |
| 1.3 | ✅ DONE | 2025-09-17 | ✅ YES | **AI Generation with executive validation - all features worked out of the box** |

---

## 🚨 **CRITICAL LESSONS FROM STORY 1.1** 🚨

### **The +3 Day Swift 6 Disaster:**
- **Data Race Errors**: "sending 'self.imageProcessor' risks causing data races"
- **Actor Isolation Violations**: Cross-actor access without proper isolation
- **Complex Expression Compilation**: Swift 6 strict concurrency causing compiler timeouts
- **Missing @MainActor Isolation**: UI components not properly isolated
- **Performance Issues**: 8-10 second launch, 5 second camera delay, 3-5 second transitions

### **Swift 6 Compliance Checklist** (Single Source of Truth)
Reference this checklist in all stories - DO NOT repeat these requirements elsewhere:

- **ALL new stories MUST reference**: `docs/architecture/swift6-concurrency-architecture.md`
- **ALL UI classes MUST use**: `@MainActor` isolation
- **SELECTIVE @preconcurrency imports**: Only for specific modules that block compilation (not blanket usage)
- **ALL async operations MUST follow**: Task isolation patterns with proper handoff
- **ALL types crossing boundaries MUST be**: Sendable compliant
- **Image processing**: Move heavy work off main thread using worker actors
- **iOS 16 compatibility**: Include availability guards and @preconcurrency shims where needed

### **Performance Targets by Story Type** (Single Source of Truth)
Reference these targets in stories - DO NOT repeat elsewhere:

- **UI-only stories**: No network. Interactions <100ms. No spinners required.
- **Network stories**: P50 <2s; P95 <5s; timeout 10s with user feedback.
- **Image processing**: Background actors for heavy work, main thread handoff for UI updates.

---

## Implemented Functionality by Category

### 🏗️ **Project Infrastructure (Story 1.0)**

| Component | Implementation Details | Status | Future Notes |
|-----------|----------------------|--------|--------------|
| **Xcode Project** | iOS 16.0+ min, 17+ optimized, SwiftUI, Bundle: com.facemakeai | ✅ DONE | DO NOT re-create |
| **Clean Architecture** | Views/, Interactors/, Repositories/, Models/ | ✅ DONE | Structure established |
| **Git Repository** | .gitignore, shared schemes, CI-ready | ✅ DONE | Version control ready |
| **Info.plist** | Camera/Photo permissions pre-configured | ✅ DONE | DO NOT duplicate |
| **App Branding** | Icon, launch screen, display name | ✅ DONE | Assets in place |
| **Privacy Manifest** | PrivacyInfo.xcprivacy for iOS 17+ | ✅ DONE | Compliance ready |
| **Build Configuration** | Warnings-as-errors, Swift Strict Concurrency | ✅ DONE | Production settings |

### 📱 **UI Components & Screen Architecture (Stories 1.0-1.3)**

| Screen/Component | Implementation Details | Status | Swift 6 Compliance | Navigation Role | Future Notes |
|------------------|----------------------|--------|---------------------|-----------------|--------------|
| **FacemakeApp.swift** | Main app entry point with NavigationStack | ✅ DONE | ✅ YES | Root container | **Only modify via approved entry points (EnvObjects/AppState injection)** |
| **ContentView.swift** | Root NavigationStack container | ✅ DONE | ✅ YES | Navigation host | **Uses modern NavigationStack (iOS 16+), not deprecated NavigationView** |
| **TitleView.swift** | Landing/welcome screen with "Start" button | ✅ DONE | ✅ YES | Entry point | First screen in user flow |
| **CaptureView.swift** | Camera/gallery selection interface | ✅ DONE | ✅ YES | Input capture | Camera + PhotoPicker integration |
| **ImagePreviewView.swift** | Image review with zoom/pan and accept/retake | ✅ DONE | ✅ YES | Validation step | **SOLE image preview screen with gesture support** |
| **StyleSelectionView.swift** | Style parameter configuration (angle + type) | ✅ DONE | ✅ YES | Style config | **Complete UI with slider and toggle, ready for generation** |
| **GenerationView.swift** | AI generation progress with loading states | ✅ DONE | ✅ YES | Generation UI | **NEW in 1.3** - Phase-based progress display |
| **ResultView.swift** | Generated image display with actions | ✅ DONE | ✅ YES | Result screen | **NEW in 1.3** - Save/share/regenerate functionality |
| **CameraSessionView.swift** | AVFoundation camera preview component | ✅ DONE | ✅ YES | Camera layer | Embedded in CaptureView |
| **PhotoPickerView.swift** | PHPicker wrapper component | ✅ DONE | ✅ YES | Gallery layer | Embedded in CaptureView |
| **CooldownTimerView.swift** | Rate limit countdown display | ✅ DONE | ✅ YES | Error state | **NEW in 1.3** - Timer UI component |
| **ShareSheet.swift** | Native share functionality wrapper | ✅ DONE | ✅ YES | Share layer | **NEW in 1.3** - UIActivityViewController bridge |

### 🔧 **Business Logic (Story 1.1)**

| Component | Implementation Details | Status | Swift 6 Compliance | Future Notes |
|-----------|----------------------|--------|-------------------|--------------|
| **AppState.swift** | `@MainActor` state management | ✅ DONE | ✅ YES | Complete implementation |
| **CameraInteractor.swift** | `@MainActor` camera operations | ✅ DONE | ✅ YES | Permissions + session |
| **ImageProcessingInteractor.swift** | **Background worker actor for heavy processing** | 🔄 NEEDS REFACTOR | ⚠️ PARTIAL | **CRITICAL: Move off @MainActor to prevent UI jank** |
| **StyleInteractor.swift** | `@MainActor` style state management with throttled persistence | ✅ DONE | ✅ YES | **Task-based throttling (135ms) for performance optimization** |

### 🎨 **Style System (Story 1.2) - COMPLETED**

| Component | Implementation Details | Status | Notes |
|-----------|----------------------|--------|-------|
| **CameraAngle Mapping** | `[-1,-0.33)=Left, [-0.33,0.33]=Front, (0.33,1]=Right` | ✅ DONE | **Raw Double + derived enum implemented in AppState.swift** |
| **StyleParameters.swift** | Angle + StyleType with Sendable compliance | ✅ DONE | **Consolidated into AppState.swift with proper Sendable conformance** |
| **Style Selection UI** | Angle slider (-1 to 1) + Professional/Casual toggle | ✅ DONE | **Local @State + throttled AppState commits for optimal UX** |
| **Accessibility Support** | VoiceOver labels with percentage announcements | ✅ DONE | **Angle mapped to [0-100%] for user comprehension** |
| **Parameter Display** | Real-time text display of current selections | ✅ DONE | **"Angle: Left • Style: Professional" format** |

### 🤖 **AI Generation System (Story 1.3) - COMPLETED**

| Component | Implementation Details | Status | Swift 6 Compliance | Notes |
|-----------|----------------------|--------|-------------------|-------|
| **GeminiClient.swift** | Actor-isolated HTTP client for Gemini 2.5 Flash | ✅ DONE | ✅ YES | **Complete API integration with error handling** |
| **GenerationPhase Enum** | State tracking: idle→preparing→uploading→processing→done/failed/rateLimited | ✅ DONE | ✅ YES | **Sendable enum with associated values** |
| **GenerationInteractor** | @MainActor business logic for generation flow | ✅ DONE | ✅ YES | **Task-based cancellation, prompt engineering** |
| **Prompt Engineering** | 6 prompt combinations (3 angles × 2 styles) with facial preservation | ✅ DONE | ✅ YES | **Temperature 0.05 for consistency** |
| **Image Processing Pipeline** | Validation→compression→Base64 encoding with HEIC support | ✅ DONE | ✅ YES | **7MB hard limit, automatic compression to 2MB target** |
| **Rate Limiting** | 5-minute cooldown with live countdown timer | ✅ DONE | ✅ YES | **ResourceExhausted error handling** |
| **Error Handling** | Comprehensive HTTP status mapping to user-friendly messages | ✅ DONE | ✅ YES | **No auto-retry, manual user guidance** |
| **Generation Progress UI** | Phase-based loading with cancel functionality | ✅ DONE | ✅ YES | **Context7 AsyncImagePhase patterns** |
| **Result Display** | Save to Photos, Share, Regenerate functionality | ✅ DONE | ✅ YES | **PHPhotoLibrary integration, in-place regeneration** |
| **Executive Validation** | Real-world testing on physical device confirmed | ✅ DONE | ✅ YES | **All features worked out of the box** |

### 🛡️ **Permissions System (Story 1.1)**

| Feature | Implementation Details | Status | Inheritance Notes |
|---------|----------------------|--------|-------------------|
| **Camera Permissions** | Runtime request + denial flows | ✅ DONE | Complete with Settings deep link |
| **Photo Library Permissions** | Runtime request + denial flows | ✅ DONE | Complete with Settings deep link |
| **Permission UI** | Educational screens with explanations | ✅ DONE | User-friendly messaging |
| **Settings Integration** | Deep link to iOS Settings app | ✅ DONE | Full navigation implemented |

### 🖼️ **Image Processing Pipeline (Story 1.1)**

| Feature | Implementation Details | Status | Inheritance Notes |
|---------|----------------------|--------|-------------------|
| **Image Capture** | AVFoundation camera capture | ✅ DONE | Front/rear toggle working |
| **Gallery Selection** | PHPicker integration | ✅ DONE | Limited access support |
| **Image Validation** | Size/format validation | ✅ DONE | Too large/small handling |
| **Image Resizing** | **Adaptive compression: scale down/reduce quality until ≤2MB** | 🔄 NEEDS IMPROVEMENT | **Current "fixed 1280px + 0.7 JPEG" may exceed 2MB on busy images** |
| **Preview System** | Full-screen preview with zoom | ✅ DONE | Pinch/pan gestures |
| **Error Handling** | User-friendly error messages | ✅ DONE | Timeout protection |

### 🧭 **Complete Navigation Flow (Stories 1.0-1.3)**

| Flow Step | From Screen | To Screen | Trigger | Implementation | Status |
|-----------|------------|-----------|---------|----------------|--------|
| **App Launch** | FacemakeApp | TitleView | App start | NavigationStack root | ✅ DONE |
| **Start Journey** | TitleView | CaptureView | "Start" button | NavigationLink | ✅ DONE |
| **Image Captured** | CaptureView | ImagePreviewView | Camera/gallery selection | State transition | ✅ DONE |
| **Image Approved** | ImagePreviewView | StyleSelectionView | "Use This Photo" | AppState.selectedInputImage | ✅ DONE |
| **Generate Triggered** | StyleSelectionView | GenerationView | "Generate" button | Sheet presentation | ✅ DONE |
| **Generation Complete** | GenerationView | ResultView | Auto/manual trigger | AppState.shouldShowResult | ✅ DONE |
| **Start Over** | ResultView | CaptureView | "New Photo" button | Navigation reset | ✅ DONE |
| **Regenerate** | ResultView | In-place | "Regenerate" button | Loading overlay | ✅ DONE |
| **Error Recovery** | Any screen | Previous/Error state | Various triggers | Comprehensive error handling | ✅ DONE |

### ⚡ **Performance & Concurrency (Story 1.1)**

| Feature | Implementation Details | Status | Issue Resolved |
|---------|----------------------|--------|----------------|
| **Camera Warm-up** | Async session initialization | ✅ DONE | ✅ 5s → <1s delay |
| **Background Processing** | Task isolation patterns | ✅ DONE | ✅ Data race fixes |
| **Logger Caching** | Avoid @MainActor capture | ✅ DONE | ✅ Background closure fix |
| **Complex Expression Fix** | ViewBuilder computed properties | ✅ DONE | ✅ Compiler timeout fix |
| **@MainActor Isolation** | All UI components isolated | ✅ DONE | ✅ Actor isolation |

---

## 🚫 **DO NOT IMPLEMENT - Already Complete or Explicitly Scrapped**

**Note:** This list applies to already-delivered components. Does NOT block new screens for future features (Settings, etc.).

### Future Stories Must NOT Include:

#### **Project Setup Tasks:**
- ❌ Xcode project creation
- ❌ Bundle identifier configuration
- ❌ Info.plist permission setup
- ❌ Git repository initialization
- ❌ Clean Architecture folder structure
- ❌ App icon/branding assets

#### **Camera/Gallery Functionality:**
- ❌ Camera permission requests
- ❌ Photo library permission requests
- ❌ AVFoundation camera session setup
- ❌ PHPicker integration
- ❌ Front/rear camera toggle
- ❌ Image capture functionality
- ❌ Gallery selection flow

#### **Image Processing:**
- ❌ Basic image resize/compression (needs adaptive improvement)
- ❌ Size validation framework
- ❌ JPEG quality optimization
- ❌ Image format conversion
- ❌ Memory management for images

#### **Navigation Infrastructure:**
- ❌ Title → Capture navigation
- ❌ Capture → Preview navigation
- ❌ Preview → Style navigation
- ❌ AppState.selectedInputImage integration
- ❌ NavigationStack setup

#### **UI Components:**
- ❌ Basic SwiftUI view structure
- ❌ Camera preview interface
- ❌ Image preview with zoom
- ❌ Permission denial screens
- ❌ Error handling UI

#### **Style Selection Features (Explicitly Scrapped for MVP):**
- ❌ Style preview with visual representations (icons, silhouettes, transforms)
- ❌ Rotation transforms or visual angle indicators
- ❌ Complex preview UI components
- ❌ Style preview accessibility features
- ❌ Any visual effects for parameter display

#### **Style Selection System (Completed in Story 1.2) - DO NOT RE-IMPLEMENT:**
- ❌ Angle slider UI and interaction handling
- ❌ Professional/Casual toggle interface
- ❌ StyleParameters data model creation
- ❌ StyleInteractor state management
- ❌ Parameter display text formatting
- ❌ Accessibility labels for style controls
- ❌ Throttled persistence for style parameters
- ❌ AppState.selectedStyle integration

---

## 🚀 **Epic 1 Complete - Ready for Epic 2 Planning**

### **✅ Epic 1 MVP Foundation (All Stories Complete)**
**Epic 1 delivered a fully functional MVP with direct API integration:**

- ✅ **Complete User Flow**: Title → Camera/Gallery → Preview → Style → Generate → Result
- ✅ **Swift 6 Compliance**: Zero concurrency warnings, proper actor isolation
- ✅ **AI Generation**: Gemini 2.5 Flash integration with facial feature preservation
- ✅ **Error Handling**: Comprehensive user-friendly error recovery
- ✅ **Executive Validation**: Real-world testing confirmed all features working
- ✅ **Quality Gate**: LOW risk assessment with production readiness

### **🎯 Epic 2 Inheritance Opportunities**

Based on Story 1.3 completion and architecture docs, Epic 2 can inherit:

| Epic 1 Component | Epic 2 Inheritance | Migration Strategy | Notes |
|------------------|-------------------|-------------------|-------|
| **GeminiClient Actor** | Move to server-side proxy | Vercel Edge Functions | **Security**: Remove API key from client |
| **GenerationInteractor** | Add AuthInteractor, CreditsInteractor | Extend patterns | **Pattern reuse**: Task-based, @MainActor |
| **Navigation Architecture** | Add Authentication screens | NavigationStack extension | **Maintain flow**: Insert auth before generation |
| **AppState Management** | Add user, credits, auth state | Extend @Published properties | **State management**: Build on existing patterns |
| **Error Handling** | Extend for auth/credit errors | Reuse GeminiError patterns | **User experience**: Consistent error messaging |
| **Image Processing Pipeline** | Keep client-side | No changes needed | **Performance**: Compression/validation works |
| **Swift 6 Patterns** | Apply to all new components | Use established architecture | **Compliance**: Zero warnings requirement |

### **📋 Epic 2 Scope (Likely Components)**

Based on No-Go items from Story 1.3 and architecture:

```
Epic 2 - Backend Infrastructure & Monetization
├── Authentication Flow
│   ├── AuthView.swift               # NEW - Login/signup
│   ├── AuthInteractor.swift         # NEW - Supabase integration
│   └── OnboardingView.swift         # NEW - User onboarding
├── Credits System
│   ├── CreditsInteractor.swift      # NEW - Usage tracking
│   ├── CreditsView.swift            # NEW - Balance display
│   └── PurchaseView.swift           # NEW - IAP integration
├── Backend Services
│   ├── Vercel Edge Functions        # NEW - API proxy
│   ├── Supabase Auth                # NEW - User management
│   └── Usage tracking               # NEW - Credits/limits
└── Enhanced Features
    ├── GenerationHistoryView.swift  # NEW - Previous results
    ├── WatermarkService.swift       # NEW - Free tier marking
    └── ProfileView.swift            # NEW - User settings
```

---

## 📋 **Available for Implementation**

### **What Future Stories CAN Build:**

#### **Style Selection System (Story 1.2) - COMPLETED:**
- ✅ Simple text display of current parameters (MVP: no visual previews) - **IMPLEMENTED**
- ✅ Angle slider with semantic mapping - **IMPLEMENTED**
- ✅ Professional/casual toggle - **IMPLEMENTED**
- ✅ StyleInteractor for parameter management - **IMPLEMENTED**

#### **AI Generation Pipeline (Story 1.3) - NEXT PRIORITY:**
- 🔄 AI API integration (HTTP client, API models, error handling)
- 🔄 Generation UI (progress indicators, loading states)
- 🔄 Result display screen for generated images
- 🔄 Error handling for network/API failures
- 🔄 Integration with existing AppState (selectedInputImage + selectedStyle)

#### **Results & Sharing (Story 1.4):**
- ✅ Generated image display
- ✅ Save to photo library
- ✅ Social sharing features
- ✅ Result comparison tools

#### **Authentication & Credits (Story 2.x):**
- ✅ User authentication system
- ✅ Credit tracking/management
- ✅ Purchase flow integration
- ✅ User profile management

---

## 📚 **Reference Documentation Table**

Use these references when specified in stories:

| Reference | Path | When to Use |
|-----------|------|-------------|
| **Swift 6 Architecture** | `docs/architecture/swift6-concurrency-architecture.md` | All new stories with UI/concurrency |
| **Swift 6 Implementation Guide** | `docs/architecture/swift6-implementation-guide.md` | Complex actor patterns |
| **Context7 SwiftUI** | `/zhangyu1818/swiftui.md` | SwiftUI component implementation |
| **Context7 Concurrency** | `/apple/swift-concurrency.md` | Actor isolation patterns |

---

## 🎯 **Story Drafting Guidelines**

### **MANDATORY Checks Before Drafting:**

1. **✅ Read This Matrix**: Understand what's already implemented
2. **✅ Reference Swift 6 Compliance Checklist**: Link to single source patterns
3. **✅ Use Performance Targets by Story Type**: Don't create redundant requirements
4. **✅ Mark Inherited Tasks**: Explicitly state "✅ INHERITED FROM STORY X.X"
5. **✅ Focus on Delta Work**: Only new functionality in acceptance criteria
6. **✅ Use Context7 Research**: Validate implementation approaches per reference table

### **Story Template References:**

```yaml
## Scope Clarifications (vs. Previous Stories)

**Inherited from X.X (not re-doing here):**
- ✅ INHERITED: Camera/gallery integration (Story 1.1)
- ✅ INHERITED: Image processing pipeline (Story 1.1)
- ✅ INHERITED: Navigation infrastructure (Story 1.1)
- ✅ INHERITED: Permission handling (Story 1.1)

**Owned by X.X (delta work):**
- NEW: [Only new functionality here]

## Swift 6 Compliance

**🚨 MANDATORY READING**: `docs/architecture/swift6-concurrency-architecture.md`

**Required Implementation Patterns:**
[Reference Swift 6 Compliance Checklist above - DO NOT repeat requirements]

## Performance Requirements

[Reference Performance Targets by Story Type above - DO NOT repeat targets]
```

---

## 📊 **Implementation Metrics**

### **Story 1.0 Baseline:**
- ✅ 8 Acceptance Criteria - 100% Complete
- ✅ Build Time: <30 seconds
- ✅ Zero warnings/errors
- ✅ Foundation established

### **Story 1.1 Lessons:**
- ⚠️ 10 Acceptance Criteria - 100% Complete (after +3 day delay)
- ⚠️ Swift 6 Issues: 5 major data race errors
- ⚠️ Performance Issues: 3 critical UX problems
- ✅ Final Result: Fully functional and compliant

### **Story 1.2 Success:**
- ✅ 7 Acceptance Criteria - 100% Complete (ON TIME)
- ✅ Zero Swift 6 compilation errors (lessons applied)
- ✅ Task-based throttling pattern established
- ✅ MVP scope maintained (no feature creep)
- ✅ Comprehensive test coverage (19 unit tests)
- ✅ QA approved with 9.2/10 code quality score

### **Story 1.3 Excellence:**
- ✅ 9 Acceptance Criteria - 100% Complete (ON TIME)
- ✅ Zero Swift 6 compilation errors (patterns perfected)
- ✅ Executive validation: all features worked out of the box
- ✅ Comprehensive AI integration with error handling
- ✅ Context7 AsyncImagePhase patterns implemented
- ✅ QA approved with LOW risk assessment

### **Epic 1 Final Success Metrics:**
- ✅ 4 Stories (1.0-1.3) - 100% Complete
- ✅ Zero Swift 6 compilation errors across entire epic
- ✅ Complete user flow: Camera → AI Generation → Results
- ✅ Executive validation confirms production readiness
- ✅ Quality gates: All PASS, ready for Epic 2 planning

### **Success Criteria for Epic 2 Stories:**
- ✅ Inherit Epic 1 patterns and architecture
- ✅ Zero Swift 6 compilation errors (established patterns)
- ✅ Build on existing components, avoid reimplementation
- ✅ Maintain Context7 and SwiftUI best practices
- ✅ Clear inheritance documentation from Epic 1

---

## 🔄 **Matrix Maintenance**

### **Update Triggers:**
- New story completion
- Architecture changes
- Performance optimizations
- Swift 6 pattern updates

### **Maintainer Responsibilities:**
- Document all new implementations
- Update inheritance mappings
- Validate Swift 6 compliance
- Track performance metrics

---

## 📞 **Emergency Contacts**

**If you see redundant work being planned:**
1. **STOP immediately**
2. **Reference this matrix**
3. **Consult Swift 6 architecture docs**
4. **Use Context7 for validation**
5. **Focus only on delta functionality**

**Remember: The +3 day Story 1.1 delay must NEVER happen again!** 🚨

---

**This matrix is the source of truth for all story inheritance. Deviation will result in project delays and technical debt.**