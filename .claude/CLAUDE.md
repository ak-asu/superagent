# Claude Code Global Instructions

## User Profile
- **Name**: MG (presyze)
- **Platform**: Windows 11 (MINGW64/Git Bash)
- **Primary Stack**: Flutter/Dart, React/TypeScript, Python, Node.js
- **IDE**: VS Code with GitHub Copilot + Claude Code

## Code Style Preferences

### General
- Write clean, self-documenting code with meaningful variable names
- Prefer functional programming patterns where appropriate
- Keep functions small and focused (single responsibility)
- Use early returns to reduce nesting
- Avoid over-engineering; solve the immediate problem first

### TypeScript/JavaScript
- Use TypeScript strict mode
- Prefer `const` over `let`, avoid `var`
- Use arrow functions for callbacks
- Destructure objects and arrays when it improves readability
- Use optional chaining (`?.`) and nullish coalescing (`??`)

### Python
- Follow PEP 8 style guide
- Use type hints for function signatures
- Prefer f-strings for string formatting
- Use list comprehensions when they're readable
- Use `pathlib` for file paths

### Flutter/Dart
- Follow Effective Dart guidelines
- Use const constructors where possible
- Prefer named parameters for clarity
- Use extension methods for utility functions
- Follow BLoC/Provider pattern for state management

## Git Commit Conventions
- Use conventional commits: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`
- Keep commits atomic and focused
- Write descriptive commit messages explaining "why" not just "what"

## Testing Preferences
- Write tests for critical business logic
- Prefer integration tests over unit tests for UI components
- Use descriptive test names that explain the expected behavior
- Mock external dependencies

## Error Handling
- Always handle errors gracefully
- Provide meaningful error messages
- Log errors with appropriate context
- Never swallow exceptions silently

## Security Practices
- Never commit secrets, API keys, or credentials
- Validate all user input
- Use parameterized queries for database operations
- Follow OWASP guidelines

## Documentation
- Add JSDoc/docstrings for public APIs
- Keep README files up to date
- Document non-obvious code with inline comments
- Prefer self-documenting code over excessive comments

## Project Structure Preferences
- Keep related files close together
- Use feature-based folder structure for large projects
- Separate concerns: UI, business logic, data access
- Keep configuration files at project root

## Communication Style
- Be concise and direct
- Explain technical decisions when asked
- Suggest improvements but respect existing patterns
- Ask clarifying questions when requirements are ambiguous

## Advanced Patterns

### TypeScript Best Practices
- **Never use `any`** - use `unknown` and type guards instead
- Type async function return values explicitly
- Use generics for reusable components
- Prefer interfaces for objects, type aliases for unions
- Use const assertions for literal types where appropriate

### Python Best Practices
- Use dataclasses or Pydantic models for structured data
- Prefer context managers (`with` statements) for resources
- Use `logging` module, not `print()` statements
- Type hints: `def process(items: list[str]) -> dict[str, int]:`
- Maximum line length: 88 characters (Black formatter)

### Flutter Best Practices
- Separate business logic from UI widgets
- Use `freezed` for immutable state classes
- Keep state minimal and derive computed values
- Avoid deeply nested widget trees - extract to separate widgets

### Database Patterns
- Use parameterized queries **ALWAYS** (never string concatenation)
- Add indexes for frequently queried columns
- Use connection pooling for better performance
- Implement proper transaction management
- Handle database connection failures gracefully

### API Design
- Follow RESTful conventions (GET, POST, PUT, DELETE)
- Use proper HTTP status codes
- Implement pagination for list endpoints
- Version APIs (`/api/v1/...`)
- Return consistent error response format

### Caching Strategies
- Cache expensive computations
- Use Redis for distributed caching
- Implement cache invalidation strategies
- Set appropriate TTL values
- Consider CDN for static assets

### Monitoring & Observability
- Log at appropriate levels (DEBUG, INFO, WARN, ERROR)
- Include correlation IDs for request tracking
- Monitor key metrics (latency, error rate, throughput)
- Set up alerts for critical issues
- Use structured logging (JSON format)

## Forbidden Practices

### Never Do These
- ❌ Use `any` type in TypeScript
- ❌ Leave `console.log` or `print()` in production code
- ❌ Commit commented-out code
- ❌ Use magic numbers without named constants
- ❌ Swallow exceptions without logging
- ❌ Write functions longer than 50 lines
- ❌ Nest more than 3 levels deep
- ❌ Mutate function parameters
- ❌ Use global variables
- ❌ Mix concerns (UI logic with business logic)
- ❌ Hardcode configuration values
- ❌ Skip error handling

## Tool Integration

### MCP Servers Available
- **filesystem**: File system operations
- **memory**: Knowledge graph for context retention
- **github**: GitHub API integration
- **postgres**: Database queries (if configured)
- **sentry**: Error tracking and monitoring
- **brave-search**: Web search capabilities

### Custom Agents Available
- **architect**: System design and architecture decisions
- **security-expert**: Security audits and vulnerability scanning
- **performance-optimizer**: Performance analysis and optimization
- **test-engineer**: Comprehensive test generation and strategy

### Workflow Triggers
- Use `/code-review` for comprehensive code review
- Use `/test-generator` for creating test suites
- Use `/document` for generating documentation
- Use `/refactor` for code restructuring
- Use `/debug` for debugging assistance
- Use `/pr-create` for pull request creation
- Use `/commit` for generating commit messages

## Context Management

### When to Read Files
- Read configuration files to understand project setup
- Review related files before making changes
- Check test files to understand expected behavior
- Examine package.json/requirements.txt/pubspec.yaml for dependencies

### When to Search
- Use semantic search for concept-based queries
- Use grep for exact string/regex matches
- Search before creating to avoid duplicates
- Find all usages before refactoring

### When to Use Terminal
- Install dependencies
- Run tests after changes
- Check git status and history
- Execute build commands
- Run linters and formatters

## Decision Framework

### When Suggesting Changes
1. Understand the existing pattern first
2. Consider backwards compatibility
3. Evaluate performance implications
4. Assess security impact
5. Think about maintainability
6. Document the rationale

### When Creating New Code
1. Follow existing project conventions
2. Write tests alongside implementation (TDD)
3. Consider error cases from the start
4. Plan for future extensibility
5. Keep it simple (YAGNI principle)
6. Document complex logic

### When Debugging
1. Reproduce the issue first
2. Check logs and error messages
3. Review recent changes
4. Verify assumptions with tests
5. Fix root cause, not symptoms
6. Add tests to prevent regression

## Output Preferences

### Code Generation
- Provide complete, runnable code
- Include necessary imports
- Add inline comments for complex logic
- Show usage examples when appropriate
- Mention required dependencies

### Explanations
- Start with high-level overview
- Break down complex concepts
- Use analogies when helpful
- Provide concrete examples
- Link to relevant documentation

### Suggestions
- Prioritize by impact
- Explain trade-offs
- Show before/after comparisons
- Consider team skill level
- Respect existing architecture
