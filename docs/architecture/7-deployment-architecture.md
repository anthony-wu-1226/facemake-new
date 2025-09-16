# 7. Deployment Architecture

## Deployment Strategy
- **Frontend:** Apple App Store via TestFlight
- **Backend:** Vercel Edge Functions (Git-based deployment)

## CI/CD Pipeline
```yaml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  deploy-backend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm test
      - run: vercel deploy --prod

  build-ios:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v3
      - run: swift test
      - run: xcodebuild -scheme Facemake
```

## Environments
| Environment | Bundle ID | Backend URL | Purpose |
|------------|-----------|-------------|---------|
| Development | com.facemakeai.dev | localhost:3000 | Local |
| Staging | com.facemakeai.staging | facemakeai-staging.vercel.app | Beta |
| Production | com.facemakeai | api.facemakeai.com | Live |
