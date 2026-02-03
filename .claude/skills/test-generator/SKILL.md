---
name: test-generator
description: Generate comprehensive unit tests for code. Use when writing tests, adding test coverage, or when the user asks to create tests for their code.
allowed-tools: Read, Write, Grep, Terminal
---

# Test Generator

Generate comprehensive tests for the specified code using the AAA (Arrange-Act-Assert) pattern.

## Framework Detection
- **TypeScript/JavaScript**: Use Jest or Vitest syntax
- **Python**: Use pytest with fixtures
- **Flutter/Dart**: Use flutter_test package

## Test Categories

### 1. Happy Path Tests
- Normal expected inputs
- Typical use cases
- Standard flow completion

### 2. Edge Cases
- Empty inputs (null, undefined, empty string, empty array)
- Boundary values (0, -1, MAX_INT, empty, single item)
- Special characters and unicode
- Very large inputs

### 3. Error Cases
- Invalid inputs (should throw or return error)
- Missing required parameters
- Network/IO failures (where applicable)
- Timeout scenarios

### 4. Integration Points
- API calls (mock external services with jest.fn() or pytest.mock)
- Database operations (mock or use test DB)
- File system operations

## Test Structure

```
describe('[Component/Function Name]', () => {
  describe('[method/scenario]', () => {
    it('should [expected behavior] when [condition]', () => {
      // Arrange
      // Act
      // Assert
    });
  });
});
```

## Best Practices
- One assertion per test when possible
- Descriptive test names that read like sentences
- Use beforeEach/afterEach for setup/teardown
- Mock external dependencies
- Test behavior, not implementation
- Keep tests independent

## Framework Detection
- Detect the testing framework from package.json or existing tests
- Use appropriate matchers and syntax for the framework
- Follow existing test patterns in the codebase
