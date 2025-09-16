# Story 1.2 PR Checklist - Critical Gates

**BLOCKING REQUIREMENTS:** All 🔴 items must pass before merge. 🟡 items should pass for production quality.

## 🔴 CRITICAL: Swift 6 Concurrency (TECH-001)
**Context:** This caused +3 day delay in Story 1.1. Zero tolerance for regression.

**🚨 QA MANDATORY: DEV MUST READ SWIFT 6 ARCHITECTURE DOCS FIRST 🚨**

**BEFORE ANY CODE IS WRITTEN:**
- [ ] **Developer has read `docs/architecture/swift6-concurrency-architecture.md` ENTIRELY**
- [ ] **Developer has read `docs/architecture/swift6-implementation-guide.md` ENTIRELY**
- [ ] **Developer confirms understanding of Swift 6 patterns**

**Required Before Merge:**
- [ ] **@MainActor on all UI components** - StyleSelectionView, router, any UI state classes
- [ ] **StyleParameters is Sendable** - Pure value type, no reference types, explicit Sendable conformance
- [ ] **Logger caching pattern** - No UI object capture in background closures
- [ ] **CI passes with strict concurrency** - Build settings include `-strict-concurrency=complete`
- [ ] **Zero isolation warnings** - Clean build output, no "sending risks data races" errors

**Verification Commands:**
```bash
# Enable strict concurrency in Xcode build settings or CLI
xcodebuild -strict-concurrency=complete
# Should build without warnings
```

---

## 🔴 CRITICAL: Slider Performance (PERF-001)
**Context:** <100ms response time requirement, avoid AppState churn during drag.

**Required Before Merge:**
- [ ] **Commit-on-drag-end only** - Use `onEditingChanged:` callback, no mid-drag AppState writes
- [ ] **Thirds mapping implemented** - Continuous value → discrete buckets (left/front/right)
- [ ] **Performance test passes** - p95 drag-end-to-settled < 100ms on mid-tier device
- [ ] **Memory test passes** - <+30MB delta after 100 slider interactions

**Implementation Pattern:**
```swift
@State private var dragValue: Double = 0.5  // UI-only state
Slider(value: $dragValue, in: 0...1, onEditingChanged: { editing in
    if !editing {  // Only write when drag ends
        appState.camAngle = snapToThird(dragValue)
    }
})
```

---

## 🟡 RECOMMENDED: Input Validation (SEC-001)
**Context:** Default values are good UX, but validate/clamp for robustness.

**Recommended Before Production:**
- [ ] **Angle clamping** - Clamp input to [-1, 1] range with `max(-1, min(1, value))`
- [ ] **Style validation** - Ensure bgStyle/styleID are non-empty strings
- [ ] **Error handling** - Invalid input → friendly toast + revert to last-good
- [ ] **Fuzz testing** - Automated tests inject bad values, verify they never reach generator

---

## 🟡 RECOMMENDED: Basic Accessibility (BUS-001)
**Context:** Two free wins to avoid App Store dings.

**Quick Wins:**
- [ ] **Primary controls labeled** - `.accessibilityLabel` on slider, toggle, buttons
- [ ] **Large text tested** - Manual pass with iOS accessibility text sizes, no clipping

**Test:** Enable VoiceOver, verify key controls are readable.

---

## 🟢 NICE-TO-HAVE: State Machine (DATA-001)
**Context:** Clean navigation flow, prevent state desync.

**Implementation:**
```swift
enum Flow { case pickingInput, choosingStyle, processing, done }

@MainActor final class AppState: ObservableObject {
    @Published var flow: Flow = .pickingInput

    func confirmImage(_ img: UIImage) {
        selectedInputImage = img
        flow = .choosingStyle  // Explicit transition
    }
}
```

---

## Code Review Focus Areas

### 1. **Swift 6 Patterns** (Reviewer Priority #1)
- All `@MainActor` annotations present and correct
- No cross-actor data sharing without `await`
- Sendable conformance explicit, not inferred
- Clean build with strict concurrency

### 2. **Performance Patterns** (Reviewer Priority #2)
- No AppState mutations in slider drag callbacks
- Single write on drag completion
- Performance measurements included in PR

### 3. **Error Handling** (Reviewer Priority #3)
- Input validation with user-friendly errors
- Graceful degradation, no crashes on bad input

---

## Pre-merge Verification Script

```bash
# 1. Clean build with strict concurrency
xcodebuild clean build -strict-concurrency=complete

# 2. Run performance tests
xcodebuild test -only-testing:FacemakeUITests/StyleSelectionPerformanceTests

# 3. Basic accessibility check
# (Manual: Enable VoiceOver, test slider + toggle)

# 4. Memory leak check
# (Manual: Profile in Instruments, 100x slider interactions)
```

---

## Sign-off Required

- [ ] **Developer:** All critical items implemented and tested
- [ ] **Code Reviewer:** Swift 6 patterns verified, performance acceptable
- [ ] **QA (Quinn):** Risk assessment addressed, test cases pass

**Remember:** Story 1.1's +3 day Swift 6 delay must not happen again. When in doubt, over-comply with concurrency patterns.