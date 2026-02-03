---
name: document
description: Generate documentation for code including JSDoc, docstrings, README sections, and API docs. Use when adding documentation to code.
allowed-tools: Read, Write, Grep
---

# Documentation Generator

Generate appropriate documentation for the specified code following project standards.

## Documentation Types

### Function/Method Documentation

**JavaScript/TypeScript (JSDoc):**
```javascript
/**
 * Brief description of what the function does (explain WHY, not just WHAT).
 *
 * @param {string} paramName - Description of the parameter
 * @param {Object} options - Configuration options
 * @param {boolean} [options.flag=false] - Optional flag description
 * @returns {Promise<ResultType>} Description of return value
 * @throws {ErrorType} When this error occurs
 * @example
 * const result = await functionName('value', { flag: true });
 * console.log(result); // { success: true }
 */
```

**Python (Docstrings - Google Style):**
```python
def function_name(param: str, options: dict = None) -> Result:
    """Brief description of what the function does.

    Args:
        param: Description of the parameter.
        options: Configuration options.
            - flag: Optional flag description.

    Returns:
        Description of the return value.

    Raises:
        ErrorType: When this error occurs.

    Example:
        >>> result = function_name('value', {'flag': True})
    """
```

### Class Documentation
- Describe the purpose of the class
- Document constructor parameters
- List public methods and properties
- Include usage example

### API Endpoint Documentation
```markdown
## Endpoint Name

`METHOD /path/to/endpoint`

Description of what this endpoint does.

### Request
- **Headers**: Required headers
- **Body**: Request body schema
- **Query Params**: URL parameters

### Response
- **200**: Success response schema
- **400**: Error response schema

### Example
```curl
curl -X POST /api/endpoint -d '{"key": "value"}'
```
```

## Guidelines
- Document the "why" not just the "what"
- Include examples for complex functionality
- Keep descriptions concise but complete
- Update documentation when code changes
- Use consistent formatting throughout
