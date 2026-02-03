---
applyTo: "**/backend/**,**/api/**,**/server/**"
---

# Backend/API Guidelines

## API Structure
- Use RESTful conventions for HTTP endpoints
- Organize routes by resource: `/api/v1/users`, `/api/v1/posts`
- Use proper HTTP methods: GET (read), POST (create), PUT/PATCH (update), DELETE (remove)
- Version APIs from the start: `/api/v1/`, `/api/v2/`

## Request/Response Patterns
- Always return consistent response structure:
  ```json
  {
    "success": true,
    "data": { ... },
    "error": null
  }
  ```
- Use appropriate HTTP status codes:
  - 200: Success
  - 201: Created
  - 400: Bad Request
  - 401: Unauthorized
  - 403: Forbidden
  - 404: Not Found
  - 500: Internal Server Error

## Validation & Security
- Validate all input at the API boundary
- Use schema validation libraries (Joi, Yup, Pydantic)
- Sanitize user input to prevent injection attacks
- Rate limit endpoints to prevent abuse
- Require authentication for protected routes
- Use parameterized queries for database operations

## Error Handling
- Never expose internal errors to clients
- Log detailed errors server-side with context
- Return user-friendly error messages
- Use custom error classes for different error types
- Include error codes for client-side handling

## Database Access
- Use connection pooling for performance
- Implement proper transaction management
- Use migrations for schema changes
- Index frequently queried fields
- Avoid N+1 query problems

## Node.js/Express Specific
```typescript
// Middleware pattern
app.use(authenticateUser);
app.use(validateRequest);

// Async error handling
const asyncHandler = (fn: Function) => (req: Request, res: Response, next: NextFunction) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};
```

## Python/FastAPI Specific
```python
# Dependency injection pattern
@app.get("/users/{user_id}")
async def get_user(
    user_id: int,
    db: Session = Depends(get_db),
    current_user: User = Depends(get_current_user)
):
    return await user_service.get_user(db, user_id)
```

## Testing
- Write integration tests for all endpoints
- Test success and error cases
- Mock external service calls
- Test authentication and authorization
- Use test databases, never production
