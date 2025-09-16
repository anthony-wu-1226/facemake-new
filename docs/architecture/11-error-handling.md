# 11. Error Handling

## Error Response Format
```typescript
{
  error: {
    code: string,
    message: string,
    details?: object,
    timestamp: string,
    requestId: string
  }
}
```

## Error Codes
- UNAUTHORIZED: Invalid/missing token
- CREDITS_EXHAUSTED: No credits remaining
- GENERATION_FAILED: Gemini API error
- RATE_LIMITED: Too many requests
