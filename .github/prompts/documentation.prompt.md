# API Documentation Generator

Generate comprehensive API documentation for the selected code or file.

## Instructions

When invoked with `/documentation`, analyze the code and generate:

### 1. Overview
- Purpose and functionality summary
- Main use cases
- Dependencies and prerequisites

### 2. API Reference

For each function/method/endpoint:

**Function Signature**
```
functionName(param1: Type, param2: Type): ReturnType
```

**Description**
Clear explanation of what the function does.

**Parameters**
- `param1` (Type): Description of parameter purpose and constraints
- `param2` (Type): Description of parameter purpose and constraints

**Returns**
- `ReturnType`: Description of return value

**Throws**
- `ErrorType`: When this error occurs

**Examples**
```typescript
// Example usage
const result = await functionName('value1', 'value2');
console.log(result); // Expected output
```

### 3. For REST APIs

**Endpoint**: `POST /api/v1/resource`

**Authentication**: Required/Optional

**Request Body**
```json
{
  "field1": "string",
  "field2": "number"
}
```

**Response**
```json
{
  "success": true,
  "data": { ... }
}
```

**Status Codes**
- 200: Success
- 400: Bad Request - invalid input
- 401: Unauthorized
- 404: Resource not found
- 500: Internal Server Error

**Rate Limiting**: X requests per minute

### 4. Code Examples

Provide realistic examples showing:
- Basic usage
- Error handling
- Edge cases
- Integration patterns

### 5. Best Practices

Document:
- Recommended usage patterns
- Common pitfalls to avoid
- Performance considerations
- Security considerations

## Output Format

Generate documentation in Markdown format suitable for:
- README files
- API documentation sites
- JSDoc/docstring comments
- OpenAPI/Swagger specifications

## For JSDoc/Docstrings

Generate inline documentation comments:

**TypeScript/JavaScript (JSDoc)**
```typescript
/**
 * Fetches user profile data from the API.
 * 
 * @param userId - Unique identifier for the user
 * @param options - Optional fetch configuration
 * @returns Promise resolving to user profile
 * @throws {ApiError} When user is not found or API is unavailable
 * @example
 * const user = await getUserProfile('123');
 * console.log(user.name);
 */
```

**Python (docstring)**
```python
def get_user_profile(user_id: str, options: dict = None) -> UserProfile:
    """
    Fetch user profile data from the API.
    
    Args:
        user_id: Unique identifier for the user
        options: Optional configuration dictionary
        
    Returns:
        UserProfile object containing user data
        
    Raises:
        ApiError: When user is not found or API is unavailable
        
    Example:
        >>> user = get_user_profile('123')
        >>> print(user.name)
    """
```

## Usage

1. Select the code/file you want to document
2. Run `/documentation`
3. Review and customize the generated documentation
4. Add any domain-specific details
