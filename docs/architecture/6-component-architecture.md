# 6. Component Architecture

## iOS App Components (Clean Architecture)

### Presentation Layer - Views
- TitleView, CaptureView, StyleSelectionView, ResultView
- SwiftUI, Combine for reactive updates

### Business Logic Layer - Interactors
- AuthInteractor, GenerationInteractor, CreditsInteractor
- Swift async/await, Combine publishers

### Data Access Layer - Repositories
- GeminiRepository, AuthRepository, UserRepository
- URLSession, Supabase Swift SDK

### Shared State - AppState
```swift
class AppState: ObservableObject {
    @Published var isAuthenticated: Bool
    @Published var user: User?
    @Published var creditsRemaining: Int
    @Published var generationInProgress: Bool
    @Published var lastGeneratedImage: UIImage?
}
```

## Backend Components

### API Gateway Function
- Route and authenticate requests
- TypeScript, Vercel Edge Runtime

### Generation Service
- Construct prompts and call Gemini 2.5 Flash
- Google AI SDK

### Credits Manager
- Single atomic Supabase RPC function
- No locking needed - simple SQL decrement
```sql
-- Supabase RPC: decrement_credits
CREATE OR REPLACE FUNCTION decrement_credits(user_id UUID)
RETURNS INTEGER AS $$
  UPDATE credits_balance
  SET credits_remaining = credits_remaining - 1
  WHERE user_id = $1 AND credits_remaining > 0
  RETURNING credits_remaining;
$$ LANGUAGE sql SECURITY DEFINER;
```
