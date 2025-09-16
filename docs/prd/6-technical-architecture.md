# 6. Technical Architecture

## 6.1 Technology Stack

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

## 6.2 System Architecture

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

## 6.3 Data Flow

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

## 6.4 Repository Structure
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
