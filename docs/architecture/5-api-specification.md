# 5. API Specification

## REST API (OpenAPI 3.0)
```yaml
openapi: 3.0.3
info:
  title: Facemake API
  version: 1.0.0

components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

paths:
  /generate:
    post:
      summary: Generate professional headshot
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                image:
                  type: string
                  format: base64
                angleValue:
                  type: number
                  minimum: -1
                  maximum: 1
                backgroundType:
                  type: string
                  enum: [professional, casual]
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                type: object
                properties:
                  success:
                    type: boolean
                  imageUrl:
                    type: string
                  creditsRemaining:
                    type: integer
```

## Rate Limiting & Timeouts
- 5 requests/minute per user (authenticated)
- 20 requests/hour per IP (unauthenticated)
- 1 concurrent request per user
- **Gemini API timeout:** 30 seconds
- **API route timeout:** 60 seconds
- **Client timeout:** 65 seconds (buffer for network)
