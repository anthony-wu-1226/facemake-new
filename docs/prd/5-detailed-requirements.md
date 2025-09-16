# 5. Detailed Requirements

## 5.1 Functional Requirements

### 4.1.1 Image Capture & Input
| Requirement | Priority | Epic |
|-------------|----------|------|
| Camera integration for live capture | P0 | 1 |
| Photo library selection | P0 | 1 |
| Image preview before processing | P0 | 1 |
| Automatic image resizing (max 2MB) | P0 | 2 |

### 4.1.2 AI Processing
| Requirement | Priority | Epic |
|-------------|----------|------|
| Gemini 2.5 Flash API integration | P0 | 1 |
| 6 pre-engineered prompts | P0 | 1 |
| Server-side API proxy | P0 | 2 |
| Processing time < 60 seconds | P0 | 1 |

### 4.1.3 User Management
| Requirement | Priority | Epic |
|-------------|----------|------|
| Email/password authentication | P0 | 2 |
| JWT session management | P0 | 2 |
| Credit tracking (3/day free) | P0 | 2 |
| Subscription status management | P0 | 2 |

### 4.1.4 Monetization
| Requirement | Priority | Epic |
|-------------|----------|------|
| Apple In-App Purchase | P0 | 2 |
| $14.99/month Pro tier | P0 | 2 |
| Receipt validation | P0 | 2 |
| Watermark for free tier ("Facemake" bottom-right, 30% opacity, 3% image width) | P0 | 2 |

## 5.2 Non-Functional Requirements

### 4.2.1 Performance
- Image generation: < 60 seconds
- App response time: < 100ms
- API timeout: 120 seconds default
- Concurrent user support: 100+

### 4.2.2 Reliability
- Best effort reliability (downtime risk accepted for MVP)
- Graceful error handling with user-friendly messages
- No automatic retry (complexity avoided for MVP)
- Offline detection and clear messaging
- Minimal telemetry: crash logs + generation duration (no PII)

### 4.2.3 Security
- No client-side API keys (Epic 2)
- Encrypted user data storage
- Secure JWT authentication
- Apple receipt validation (on-demand only)
- Note: Server-to-server Apple notifications for future versions

### 4.2.4 Usability
- 3-tap primary flow
- Single-hand operation
- Clear visual feedback
- Intuitive error messages

---
