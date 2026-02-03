# Project-Specific Copilot Instructions

## Project Context
- **User**: MG (presyze)
- **Platform**: Windows 11 (MINGW64/Git Bash)
- **Primary Stack**: Flutter/Dart, React/TypeScript, Python, Node.js
- **IDE**: VS Code with GitHub Copilot + Claude Code

## Code Style Preferences

### General Principles
- Write clean, self-documenting code with meaningful variable names
- Prefer functional programming patterns where appropriate
- Keep functions small and focused (single responsibility principle)
- Use early returns to reduce nesting depth
- Avoid over-engineering; solve the immediate problem first
- No magic numbers - use named constants

### Naming Conventions
- **Variables & Functions**: camelCase (`getUserData`, `isActive`)
- **Classes & Types**: PascalCase (`UserProfile`, `ApiResponse`)
- **Constants**: SCREAMING_SNAKE_CASE (`MAX_RETRIES`, `API_BASE_URL`)
- **Private members**: Prefix with underscore where appropriate (`_internalState`)
- Use descriptive, meaningful names that reveal intent

### File Organization
- Group related files together by feature/domain
- Keep files focused and small (<300 lines when possible)
- Use index files for clean barrel exports
- Separate concerns: UI, business logic, data access
- Keep configuration files at project root

### Import Standards
- Order: external packages → internal modules → relative imports
- Group imports by type (React, libraries, components, utils, types)
- Use absolute imports where possible to avoid `../../..` chains
- Avoid circular dependencies

## TypeScript/JavaScript

### Type Safety
- Use TypeScript strict mode always
- **Never use `any`** - use `unknown` if type is truly unknown, then narrow with type guards
- Prefer `const` over `let`, never use `var`
- Use type guards for narrowing (`typeof`, `instanceof`, custom guards)
- Prefer interfaces for objects, type aliases for unions/intersections
- Use const assertions for literal types where appropriate

### Modern Patterns
- Use arrow functions for callbacks and short functions
- Destructure objects and arrays when it improves readability
- Use optional chaining (`?.`) and nullish coalescing (`??`)
- Prefer async/await over `.then()` chains
- Use `Promise.all()` for parallel async operations
- Type async function return values explicitly

### React/TSX Specific
- Use functional components with hooks (no class components)
- Type component props with interfaces, not inline types
- Use React.FC sparingly - prefer explicit return types
- Type event handlers properly (`React.ChangeEvent<HTMLInputElement>`)
- Extract logic into custom hooks for reusability
- Use generics for reusable components

## Python

### Style Guide
- Follow PEP 8 style guide strictly
- Use type hints for all function signatures
- Prefer f-strings for string formatting (no `%` or `.format()`)
- Use list/dict comprehensions when they remain readable
- Use `pathlib.Path` for file system operations (not `os.path`)
- Maximum line length: 88 characters (Black formatter standard)

### Best Practices
- Use dataclasses or Pydantic models for structured data
- Prefer context managers (`with` statements) for resource management
- Use `logging` module, not `print()` statements
- Type hints: `def process_data(items: list[str]) -> dict[str, int]:`

## Flutter/Dart

### Dart Guidelines
- Follow Effective Dart guidelines
- Use `const` constructors wherever possible for performance
- Prefer named parameters for functions with multiple arguments
- Use extension methods for utility functions
- Avoid deeply nested widget trees - extract to separate widgets
- Use `final` for immutable variables

### State Management
- Follow BLoC pattern or Provider pattern consistently
- Keep state minimal and derive computed values
- Separate business logic from UI widgets
- Use `freezed` for immutable state classes

## Git Commit Conventions

### Conventional Commits
Use conventional commit format: `type(scope): description`

**Types:**
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `refactor:` - Code refactoring (no functional changes)
- `test:` - Adding or updating tests
- `chore:` - Maintenance tasks, dependencies
- `perf:` - Performance improvements
- `style:` - Code style/formatting changes

**Guidelines:**
- Keep commits atomic and focused on one change
- Write descriptive messages explaining "why" not just "what"
- Use imperative mood ("Add feature" not "Added feature")
- Limit first line to 72 characters
- Add body for complex changes

**Examples:**
```
feat(auth): add JWT token refresh mechanism
fix(api): handle null response in user endpoint
docs(readme): update installation instructions
refactor(utils): extract validation logic to separate module
```

## Error Handling

### General Principles
- Always handle errors gracefully - never swallow exceptions silently
- Provide meaningful, user-friendly error messages
- Log errors with appropriate context (stack traces, user actions)
- Use custom error classes for domain-specific errors
- Validate all user input at boundaries

### TypeScript
```typescript
try {
  await riskyOperation();
} catch (error) {
  if (error instanceof ValidationError) {
    // Handle specific error type
  }
  logger.error('Operation failed', { error, context });
  throw new AppError('User-friendly message', error);
}
```

### Python
```python
try:
    result = risky_operation()
except ValueError as e:
    logger.error(f"Validation failed: {e}", exc_info=True)
    raise CustomError("User-friendly message") from e
```

## Testing Requirements

### Coverage & Standards
- Minimum 80% code coverage for business logic
- Write tests for critical paths and edge cases
- Prefer integration tests over unit tests for UI components
- Use descriptive test names that explain expected behavior
- Mock external dependencies (APIs, databases, file system)

### Framework-Specific
- **TypeScript/JavaScript**: Jest or Vitest with `@testing-library`
- **Python**: pytest with fixtures and parametrize
- **Flutter/Dart**: flutter_test with widget testing

### Test Structure
```typescript
describe('UserService', () => {
  it('should return user data when ID exists', async () => {
    // Arrange
    const userId = '123';
    // Act
    const result = await service.getUser(userId);
    // Assert
    expect(result).toBeDefined();
    expect(result.id).toBe(userId);
  });
});
```

## Security Practices

### Critical Rules
- **Never commit secrets, API keys, credentials, or tokens**
- Store sensitive data in `.env` files (add to `.gitignore`)
- Validate and sanitize all user input
- Use parameterized queries for database operations (prevent SQL injection)
- Follow OWASP Top 10 guidelines
- Use HTTPS for all external API calls
- Implement proper authentication and authorization checks

## Documentation

### Code Documentation
- Add JSDoc/docstrings for all public APIs and exported functions
- Document non-obvious code with inline comments
- Keep README files up to date with setup instructions
- Prefer self-documenting code over excessive comments
- Document "why" not "what" in comments

### API Documentation
```typescript
/**
 * Fetches user profile data from the API.
 * 
 * @param userId - Unique identifier for the user
 * @param options - Optional fetch configuration
 * @returns Promise resolving to user profile
 * @throws {ApiError} When user is not found or API is unavailable
 */
async function getUserProfile(userId: string, options?: FetchOptions): Promise<UserProfile>
```

## Do NOT

### Forbidden Practices
- ❌ Use `any` type in TypeScript (use `unknown` instead)
- ❌ Leave `console.log` or `print()` statements in production code
- ❌ Commit commented-out code (use git history instead)
- ❌ Use magic numbers without named constants
- ❌ Swallow exceptions without logging
- ❌ Write functions longer than 50 lines (extract to smaller functions)
- ❌ Nest more than 3 levels deep (use early returns or extract functions)
- ❌ Mutate function parameters
- ❌ Use global variables
- ❌ Mix concerns (UI logic with business logic)
