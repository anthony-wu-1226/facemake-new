# 12. Monitoring & Observability

## Frontend Monitoring (iOS)
```swift
// Crashlytics integration for crash reporting
import FirebaseCrashlytics

// Log custom events
Crashlytics.crashlytics().log("Generation started")
Crashlytics.crashlytics().setCustomValue(angleValue, forKey: "angle_value")

// Track non-fatal errors
Crashlytics.crashlytics().record(error: generationError)
```

## Backend Monitoring (Vercel)
```typescript
// Built-in Vercel Analytics
export async function generateHandler(req: Request, ctx: RequestContext) {
  const startTime = Date.now()

  try {
    const result = await generateImage(req)

    // Log metrics to Vercel Analytics (NO base64 images!)
    console.log(JSON.stringify({
      event: 'generation_success',
      duration: Date.now() - startTime,
      credits: req.body.creditsRemaining
      // NEVER log req.body.image - it's base64!
    }))

    return result
  } catch (error) {
    // Error tracking with context
    ctx.waitUntil(
      fetch('https://error-tracking.vercel.app', {
        method: 'POST',
        body: JSON.stringify({
          error: error.message,
          stack: error.stack,
          url: req.url,
          timestamp: new Date().toISOString()
        })
      })
    )
    throw error
  }
}
```

## Key Metrics Dashboard
| Metric | Target | Alert Threshold |
|--------|--------|-----------------|
| Generation Success Rate | > 95% | < 90% |
| API Response Time | < 2s | > 5s |
| Gemini API Latency | < 30s | > 45s |
| Credit Transaction Success | > 99% | < 95% |
| Daily Active Users | Growth | -20% WoW |

## Alert Configuration
- **Critical:** Generation API down, Auth service failure
- **Warning:** High error rate, slow response times
- **Info:** Daily usage reports, credit depletion warnings
