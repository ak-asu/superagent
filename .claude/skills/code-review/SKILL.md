---
name: code-review
description: Perform a comprehensive code review. Use when reviewing code changes, pull requests, or when the user asks to review their code for quality, bugs, security issues, or improvements.
allowed-tools: Read, Grep, Glob
---

# Code Review

Perform a thorough code review covering these areas:

## 1. Correctness
- Logic errors and edge cases
- Off-by-one errors
- Null/undefined handling
- Error handling completeness
- Type safety (TypeScript strict mode violations)

## 2. Security
- **CRITICAL**: No hardcoded secrets, API keys, or credentials
- Input validation and sanitization
- SQL injection vulnerabilities (use parameterized queries)
- XSS vulnerabilities (sanitize HTML output)
- CSRF protection for state-changing operations
- Authentication/authorization issues
- Sensitive data exposure in logs/errors

## 3. Performance
- N+1 query problems (use JOINs or eager loading)
- Unnecessary loops or iterations
- Memory leaks (event listeners, subscriptions)
- Inefficient algorithms (check Big O complexity)
- Missing indexes on frequently queried fields

## 4. Code Quality
- Code duplication (DRY violations)
- Single responsibility principle
- Naming conventions
- Code readability
- Unnecessary complexity

## 5. Best Practices
- Framework-specific patterns
- Error handling patterns
- Logging and observability
- Testing considerations

## Output Format

For each issue found, provide:
1. **Location**: File and line number
2. **Severity**: Critical / High / Medium / Low
3. **Issue**: Clear description of the problem
4. **Suggestion**: Specific fix or improvement

End with a summary of:
- Total issues by severity
- Overall code quality assessment
- Top 3 priority items to address
