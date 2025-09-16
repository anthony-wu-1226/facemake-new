# 10. Development Workflow

## Local Setup
```bash
# Backend
npm install
npm run dev

# iOS
cd ios
open Facemake.xcodeproj
```

## Testing Strategy

### iOS Testing (Swift Testing + XCTest)
```swift
// Using Swift Testing for unit tests
import Testing

@Test func generatePromptFormatting() {
    let interactor = GenerationInteractor()
    let prompt = interactor.buildPrompt(angleValue: 0.5, background: .professional)
    #expect(prompt.contains("professional"))
    #expect(prompt.contains("front-facing"))
}

@Test("Credit validation", arguments: [0, 1, 2, 3])
func creditDeductionLogic(credits: Int) {
    let creditsManager = CreditsInteractor()
    #expect(creditsManager.canGenerate(credits: credits) == (credits > 0))
}
```

### Backend Testing (Vitest)
```typescript
// Edge function tests
import { describe, it, expect } from 'vitest'
import { generateHandler } from '../api/generate'

describe('Generation API', () => {
  it('validates request format', async () => {
    const response = await generateHandler({
      body: { angleValue: 2 } // Invalid range
    })
    expect(response.status).toBe(400)
  })
})
```

### E2E Testing Plan
- **TestFlight Beta:** 20-50 internal testers
- **Success Metrics:** < 60s generation, < 5% error rate
- **Manual QA:** Core flows on iPhone SE/14/15 Pro
