# 9. Security & Performance

## Security
- JWT storage in iOS Keychain
- Server-side API key management
- Input validation and rate limiting
- No image storage (privacy by design)
- **Critical:** Disable request body logging for /generate endpoint
- **Watermark:** Client-side only for MVP (temporary)

## Privacy & Terms
- Stub pages hosted on Vercel
- Simple claims: "We don't store photos"
- Error logs scrubbed of PII
- Preview builds may log errors (disclosed)

## Performance
- Image compression before upload (max 2MB)
- Edge location auto-selection
- 60-second generation target (30s Gemini + overhead)
- Minimal telemetry (crash logs only)

## IAP Implementation (iOS)
```swift
// StoreKit 2 - Good enough for MVP
import StoreKit

class IAPManager {
    func purchase() async throws {
        let product = try await Product.products(for: ["com.facemakeai.pro"]).first
        let result = try await product?.purchase()
        // Basic validation, server-side receipt validation can wait
    }

    func restorePurchases() async {
        // Essential for App Store approval
        for await result in Transaction.currentEntitlements {
            // Update subscription status
        }
    }
}
```
