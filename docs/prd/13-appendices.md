# 13. Appendices

## 13.1 Prompt Engineering Templates (6 Core Styles)

**Style 1: Professional Front-Facing**
```
Generate a professional headshot of the person in this image:
- Direct front-facing angle, shoulders square to camera
- Modern office background with soft bokeh
- Business professional attire (suit/blazer suggested)
- Soft studio lighting from 45-degree angle
- Confident smile, direct eye contact
- LinkedIn-appropriate, corporate styling
- Clean, polished appearance
```

**Style 2: Professional Side-Angle**
```
Generate a professional headshot of the person in this image:
- 45-degree side angle, face turned toward camera
- Neutral gray or white backdrop
- Business professional attire
- Dramatic side lighting for depth
- Thoughtful, focused expression
- Executive portrait style
- Sharp, high-contrast details
```

**Style 3: Professional Three-Quarter**
```
Generate a professional headshot of the person in this image:
- Three-quarter view angle (between front and profile)
- Blurred conference room or bookshelf background
- Business casual attire (dress shirt/blouse)
- Natural window lighting effect
- Approachable, warm expression
- Modern corporate headshot style
- Balanced, symmetrical composition
```

**Style 4: Casual Front-Facing**
```
Generate a professional headshot of the person in this image:
- Direct front-facing angle, relaxed posture
- Outdoor or coffee shop background, softly blurred
- Smart casual attire (polo, casual button-up)
- Natural, warm lighting
- Genuine, friendly smile
- Approachable startup/tech style
- Vibrant, engaging appearance
```

**Style 5: Casual Side-Angle**
```
Generate a professional headshot of the person in this image:
- 45-degree casual angle, natural head turn
- Urban or brick wall background
- Casual professional attire (sweater, casual shirt)
- Golden hour lighting effect
- Relaxed, confident expression
- Creative industry style
- Artistic, contemporary feel
```

**Style 6: Casual Three-Quarter**
```
Generate a professional headshot of the person in this image:
- Three-quarter casual angle
- Park or natural environment background, bokeh effect
- Weekend professional attire (smart casual)
- Soft, diffused natural lighting
- Easy-going, authentic expression
- Lifestyle professional style
- Warm, inviting composition
```

**Prompt Testing Requirements:**
- Each prompt must be tested with 20+ diverse faces
- Document success rate per demographic
- Flag any consistent failures for immediate dev review
- A/B test variations if quality drops below 80% satisfaction

## 13.2 Error Messages

| Error Condition | User Message | Technical Log | Action |
|-----------------|--------------|---------------|---------|
| API timeout | "Taking a bit longer than usual..." | GEMINI_TIMEOUT_ERROR | Auto-refund credit |
| No credits | "You've used today's free photos. Upgrade to Pro for unlimited!" | CREDITS_EXHAUSTED | Show upgrade button |
| Network error | "Check your connection and try again" | NETWORK_UNAVAILABLE | Show retry button |
| Generation failed | "Let's try that again" | GENERATION_FAILED | Auto-refund credit |
| Image too large | "Photo too large. We'll resize it for you." | IMAGE_RESIZE_REQUIRED | Auto-resize and proceed |
| Invalid format | "Please use JPEG, PNG, or HEIC format" | INVALID_IMAGE_FORMAT | Return to camera |
| Multiple faces | "Please use a photo with only one person" | MULTIPLE_FACES_DETECTED | Return to camera |
| No face detected | "Couldn't find a face. Try a different photo" | NO_FACE_DETECTED | Return to camera |
| Inappropriate content | "This image cannot be processed" | CONTENT_VIOLATION | Return to camera |
| Server overloaded | "High demand right now. Please try again in a moment" | SERVER_OVERLOAD | Show retry in 30s |
| Prompt failure | "Technical issue detected. Our team has been notified" | PROMPT_GENERATION_ERROR | Auto-refund, flag for dev review |

## 13.3 Glossary
- **Epic:** Major development milestone
- **MVP:** Minimum Viable Product
- **IAP:** In-App Purchase
- **JWT:** JSON Web Token
- **P0:** Priority 0 (critical requirement)

---
