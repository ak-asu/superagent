---
name: refactor
description: Refactor code to improve quality without changing behavior. Use when code needs restructuring, simplification, or modernization while preserving functionality.
---

# Code Refactoring

Refactor the specified code following these principles:

## Refactoring Goals
1. **Readability**: Make code easier to understand
2. **Maintainability**: Make future changes easier
3. **Testability**: Make code easier to test
4. **Performance**: Improve efficiency where obvious

## Refactoring Techniques

### Extract
- Extract repeated code into functions
- Extract complex conditions into named variables
- Extract magic numbers into named constants

### Simplify
- Reduce nesting with early returns
- Replace complex conditionals with guard clauses
- Use modern language features (optional chaining, destructuring)

### Organize
- Group related code together
- Order functions logically (public before private)
- Separate concerns into modules

### Clean Up
- Remove dead code
- Remove unnecessary comments
- Improve variable/function names

## Process
1. First, understand what the code does
2. Identify specific improvements
3. Apply changes incrementally
4. Verify behavior is preserved

## Output
- Show before/after for significant changes
- Explain the reasoning for each change
- Note any behavioral changes (there should be none)
