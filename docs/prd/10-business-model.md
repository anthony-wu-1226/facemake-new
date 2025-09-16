# 10. Business Model

## 10.1 Pricing Strategy

**Free Tier:**
- 3 generations per day
- Watermarked images
- Access to all 6 styles
- Basic support

**Pro Tier ($14.99/month):**
- Unlimited generations
- No watermarks
- Priority processing
- Early access to new features

**App Store Configuration:**
- Product ID: `com.facemakeai.pro.monthly`
- Product Name: "Facemake Pro Monthly"
- Price Tier: Tier 15 ($14.99 USD)
- Auto-renewable subscription

## 10.2 Revenue Projections

**Conservative Scenario (Year 1):**
- 10,000 free users
- 5% conversion to Pro
- 500 × $14.99 = $7,495/month

**Growth Scenario (Year 1):**
- 50,000 free users
- 10% conversion to Pro
- 5,000 × $14.99 = $74,950/month

## 10.3 Cost Structure
- Gemini API: ~$0.10 per generation
  - Hard cap: 3 generations/user/day enforced by Supabase
  - Maximum theoretical cost: 10,000 users × 3 × $0.10 = $3,000/day
  - Realistic MVP cost: 50 users × 3 × $0.10 = $15/day
- Vercel hosting: $20/month
- Supabase: $25/month
- Apple fees: 30% of IAP revenue
- **Cost Protection:** Atomic credit decrements prevent race conditions

---
