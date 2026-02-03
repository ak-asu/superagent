# Bug Investigation and Fix Prompt

Use this prompt when debugging issues or fixing bugs.

## Objective
Systematically identify, analyze, and fix bugs with proper testing and documentation.

## Investigation Process

### 1. Reproduce the Issue
- Gather detailed bug report information
- Steps to reproduce
- Expected vs actual behavior
- Environment details (OS, browser, versions)
- Error messages and stack traces
- Screenshots or screen recordings

### 2. Isolate the Problem
- Identify which component/module is affected
- Check if issue is consistently reproducible
- Determine if it's a regression (when did it start?)
- Verify in different environments (dev, staging, production)
- Check if related to recent changes (git log, git blame)

### 3. Gather Context
**Files to Review:**
- [ ] The file where the error occurs
- [ ] Related test files
- [ ] Recent commits touching the affected code
- [ ] Configuration files
- [ ] Dependencies (package.json, requirements.txt)

**Logs to Check:**
- [ ] Application logs
- [ ] Browser console (for frontend issues)
- [ ] Server logs (for backend issues)
- [ ] Database logs
- [ ] Third-party service logs (Sentry, etc.)

### 4. Form Hypothesis
Based on evidence:
1. What is the root cause?
2. Why wasn't this caught earlier?
3. What are potential side effects of fixing it?
4. Are there similar issues elsewhere?

### 5. Debugging Techniques

#### Add Strategic Logging
```typescript
// TypeScript
console.log('DEBUG: Variable state before operation:', { variable, context });

// Python
import logging
logging.debug(f'Variable state: {variable}, context: {context}')

// Flutter
debugPrint('Widget state: $state');
```

#### Use Debugger
- Set breakpoints at suspected locations
- Step through code execution
- Inspect variable values
- Check call stack

#### Verify Assumptions
```typescript
// Add assertions to verify expectations
if (!user) {
  throw new Error('User should always be defined at this point');
}
```

### 6. Implement Fix

#### Fix Guidelines
- Fix the root cause, not symptoms
- Keep changes minimal and focused
- Maintain backwards compatibility when possible
- Add defensive checks if appropriate
- Consider performance implications

#### Code Review Yourself
- Does this fix address the root cause?
- Could this introduce new issues?
- Are error messages clear and actionable?
- Is the fix testable?
- Should similar code elsewhere be updated?

### 7. Prevent Regression

#### Add Tests
```typescript
// Test the specific bug scenario
describe('Bug #123: User data not loading', () => {
  it('should load user data when token is valid', async () => {
    // Arrange - set up the exact scenario that caused the bug
    const token = 'valid-token';
    
    // Act - execute the fixed code path
    const user = await loadUserData(token);
    
    // Assert - verify the fix works
    expect(user).toBeDefined();
    expect(user.id).toBe('123');
  });

  it('should handle expired token gracefully', async () => {
    const expiredToken = 'expired-token';
    await expect(loadUserData(expiredToken))
      .rejects.toThrow('Token expired');
  });
});
```

### 8. Documentation

#### Update Code Comments
```typescript
/**
 * Loads user data from the API.
 * 
 * Fixed: Bug #123 - Handle token expiration properly
 * @see https://github.com/org/repo/issues/123
 */
```

#### Commit Message Format
```
fix(auth): handle expired tokens gracefully

Previously, expired tokens caused silent failures leading to
undefined user data. Now properly catches token expiration and
throws a descriptive error.

Fixes #123
```

#### Bug Report Update
- Explain root cause
- Describe the fix
- Note any workarounds for older versions
- List affected versions
- Provide timeline for fix deployment

## Common Bug Categories

### Frontend Bugs
- **Rendering issues**: Check component lifecycle, state updates
- **Event handling**: Verify event listeners attached/removed properly
- **Memory leaks**: Check for unsubscribed observables, dangling references
- **Race conditions**: Use proper async/await, debouncing, cancellation

### Backend Bugs
- **API errors**: Check request validation, error handling
- **Database issues**: Verify queries, connections, transactions
- **Memory leaks**: Check for unclosed connections, large object retention
- **Concurrency issues**: Verify thread safety, race conditions

### Database Bugs
- **Slow queries**: Use EXPLAIN ANALYZE, add indexes
- **Deadlocks**: Review transaction isolation levels, query order
- **Data inconsistency**: Check constraint enforcement, race conditions
- **Connection pool exhaustion**: Verify connections are released

## Example Bug Fix

### Bug Report
**Title**: Users can't log in after password reset
**Steps**: 1. Reset password, 2. Try to login with new password
**Expected**: Login successful
**Actual**: "Invalid credentials" error

### Investigation
```typescript
// Check the password reset function
async function resetPassword(userId: string, newPassword: string) {
  const hash = await bcrypt.hash(newPassword, 10);
  await db.query(
    'UPDATE users SET password = $1 WHERE id = $2',
    [hash, userId]  // ❌ BUG: Column name should be password_hash
  );
}
```

### Root Cause
Column name mismatch: code uses `password` but database column is `password_hash`

### Fix
```typescript
async function resetPassword(userId: string, newPassword: string) {
  const hash = await bcrypt.hash(newPassword, 10);
  await db.query(
    'UPDATE users SET password_hash = $1 WHERE id = $2', // ✅ Fixed
    [hash, userId]
  );
}
```

### Test
```typescript
describe('Password Reset', () => {
  it('should allow login after password reset', async () => {
    const user = await createTestUser();
    const newPassword = 'NewSecurePass123!';
    
    await resetPassword(user.id, newPassword);
    const loginResult = await login(user.email, newPassword);
    
    expect(loginResult.success).toBe(true);
    expect(loginResult.token).toBeDefined();
  });
});
```

### Preventive Measures
- Add TypeScript types for database schema
- Use an ORM with type-safe column names
- Add integration tests for authentication flows

## Checklist Before Marking Fixed

- [ ] Root cause identified and documented
- [ ] Fix implemented and tested locally
- [ ] Tests added to prevent regression
- [ ] Code reviewed (or self-reviewed)
- [ ] Documentation updated
- [ ] Related issues checked for similar problems
- [ ] Changelog/release notes updated
- [ ] Bug reporter notified of fix

## Output Format

```
## Bug Analysis

**Issue**: [Brief description]
**Root Cause**: [Explanation]
**Affected Components**: [List]

## Fix Implementation

[Code changes with explanation]

## Testing

[Test cases added]

## Verification

- [ ] Original scenario now works
- [ ] No new issues introduced
- [ ] Related functionality still works
- [ ] Tests passing

## Follow-up

[Any additional improvements or monitoring needed]
```
