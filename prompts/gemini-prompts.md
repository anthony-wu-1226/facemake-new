# Gemini 2.5 Flash Prompt Engineering for FacemakeAI v3

## Base Prompt Template

```
You are an AI image processor specializing in professional headshot generation. Transform the provided photo into a high-quality headshot suitable for LinkedIn and professional use.

### Core Requirements:
- Detect and focus on the primary face in the input photo
- Preserve ALL original facial features exactly (bone structure, proportions, skin tone, hair texture/color, eye color, unique features)
- Adjust the subject's pose to face {ANGLE} naturally
- Maintain photographic realism - this should look like a real photo, not AI-generated
- Replace background with {BACKGROUND_DESC}
- Apply {LIGHTING_DESC}
- Ensure professional cropping (head and shoulders visible)
- Output quality suitable for LinkedIn profile photos

### Style Guidelines:
- Natural skin texture (avoid over-smoothing)
- Authentic expression (preserve original emotion)
- Professional but approachable appearance
- Sharp focus on face, soft background blur
- Color grading: {COLOR_STYLE}

### Error Handling:
If face detection issues occur (no face/multiple faces):
- Proceed with best attempt at subject isolation
- Flag: `warning: "Face detection uncertain - results may vary"`

### Output Specifications:
- Resolution: 1024x1024 minimum
- Format: High-quality JPEG/PNG
- Metadata: {timestamp, style, angle}
```

## The 6 Production Prompts

### 1. Professional + Front
```
Generate a professional headshot with the subject facing directly forward (front-facing angle).

Background: Clean, neutral gray studio backdrop with subtle gradient
Lighting: Balanced studio lighting with soft shadows, key light from upper left
Color grading: Cool-neutral tones, slight desaturation for corporate feel
Overall mood: Confident, trustworthy, corporate-ready
```

### 2. Professional + Left
```
Generate a professional headshot with the subject's body angled left (showing right side of face more prominently).

Background: Modern office environment with soft blur, glass and steel elements
Lighting: Professional window light from the left, fill light on right
Color grading: Cool-neutral tones with slight blue undertones
Overall mood: Dynamic, engaged, executive presence
```

### 3. Professional + Right
```
Generate a professional headshot with the subject's body angled right (showing left side of face more prominently).

Background: Contemporary workspace with blurred monitors and clean lines
Lighting: Professional window light from the right, subtle fill on left
Color grading: Neutral with slight warm accents in highlights
Overall mood: Approachable professional, modern leader
```

### 4. Casual + Front
```
Generate a casual professional headshot with the subject facing directly forward.

Background: Warm indoor space, coffee shop or co-working environment with bokeh
Lighting: Natural, warm ambient light with soft shadows
Color grading: Warm tones, enhanced golden hour feel
Overall mood: Friendly, creative, startup culture
```

### 5. Casual + Left
```
Generate a casual professional headshot with the subject's body angled left.

Background: Outdoor urban setting, blurred cityscape or brick wall
Lighting: Natural daylight, slightly overcast for even illumination
Color grading: Natural colors with slight warmth, film-inspired tones
Overall mood: Authentic, relatable, creative professional
```

### 6. Casual + Right
```
Generate a casual professional headshot with the subject's body angled right.

Background: Natural outdoor setting, park or garden with soft bokeh
Lighting: Golden hour natural light from the right side
Color grading: Warm, natural tones with enhanced greens in background
Overall mood: Approachable, genuine, work-life balance
```

## Testing Protocol

### Phase 1: Baseline Testing
Test each prompt with:
- 5 different ethnicities
- 3 age groups (20s, 30s, 40s+)
- Both genders
- Various photo qualities (selfie, portrait, group photo crop)

### Phase 2: Edge Cases
- Poor lighting input photos
- Partial face visibility
- Accessories (glasses, hats, scarves)
- Different facial hair styles
- Various clothing styles

### Phase 3: Consistency Testing
- Same person, all 6 prompts
- Verify angle changes look natural
- Ensure identity preservation across all variations

## Optimization Notes

### What to Monitor:
1. **Identity Preservation** - Face should be recognizable as same person
2. **Professional Quality** - Would a recruiter accept this on LinkedIn?
3. **Natural Appearance** - Avoid "uncanny valley" or obvious AI artifacts
4. **Style Consistency** - Each style should be distinctly different but cohesive

### Common Issues to Address:
- Over-smoothing of skin
- Unnatural eye adjustments
- Hair texture loss
- Clothing generation artifacts
- Background-subject edge blending

## Implementation in Swift

```swift
enum PhotoStyle: String {
    case professional = "Professional"
    case casual = "Casual"
}

enum PhotoAngle: String {
    case front = "Front"
    case left = "Left"
    case right = "Right"
}

func getPrompt(style: PhotoStyle, angle: PhotoAngle) -> String {
    // Return the appropriate prompt from the 6 above
    // This will be hardcoded in Epic 1
}
```

## Success Metrics

A prompt is successful when:
- 80% of users recognize themselves in the output
- 70% would use it on LinkedIn without hesitation
- Generation takes < 60 seconds
- No obvious AI artifacts visible at normal viewing distance
- Professional enough for job applications

## Future Enhancements (Post-MVP)

After collecting user feedback, we expect to add:
- Industry-specific backgrounds (tech, finance, healthcare)
- Time-of-day variations (morning, afternoon, evening)
- Seasonal adjustments
- Cultural dress code adaptations
- Team photo consistency modes