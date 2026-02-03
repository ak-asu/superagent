---
applyTo: "**/*.test.ts,**/*.test.tsx,**/*.test.js,**/*.spec.ts,**/*.spec.js,**/test_*.py,**/*_test.py,**/test/**,**/__tests__/**"
---

# Testing Guidelines

## Test Naming
- Use descriptive test names that explain expected behavior
- Pattern: `should [expected behavior] when [condition]`
- Examples:
  - `should return user data when ID exists`
  - `should throw ValidationError when email is invalid`
  - `should redirect to login when user is not authenticated`

## Test Structure (AAA Pattern)
```typescript
it('should calculate total price correctly', () => {
  // Arrange - setup test data and dependencies
  const cart = createCart();
  const item = { id: 1, price: 10, quantity: 2 };
  
  // Act - execute the behavior being tested
  cart.addItem(item);
  const total = cart.getTotal();
  
  // Assert - verify the outcome
  expect(total).toBe(20);
});
```

## Coverage Requirements
- Minimum 80% code coverage for business logic
- Test all critical paths and edge cases
- Test error handling and validation
- Test boundary conditions (empty, null, undefined, max values)

## What to Test
- ✅ Business logic and calculations
- ✅ API endpoints (request/response)
- ✅ Validation logic
- ✅ Error handling paths
- ✅ State management logic
- ✅ Component interactions (integration tests)
- ❌ Third-party libraries
- ❌ Simple getters/setters without logic

## Mocking
- Mock external dependencies (APIs, databases, file system)
- Mock time-dependent functions (`Date.now()`, timers)
- Use dependency injection for easier mocking
- Keep mocks simple and focused

## TypeScript/JavaScript (Jest/Vitest)
```typescript
describe('UserService', () => {
  let service: UserService;
  let mockRepository: jest.Mocked<UserRepository>;
  
  beforeEach(() => {
    mockRepository = {
      findById: jest.fn(),
      save: jest.fn(),
    } as any;
    service = new UserService(mockRepository);
  });
  
  it('should fetch user by ID', async () => {
    const user = { id: '123', name: 'John' };
    mockRepository.findById.mockResolvedValue(user);
    
    const result = await service.getUser('123');
    
    expect(result).toEqual(user);
    expect(mockRepository.findById).toHaveBeenCalledWith('123');
  });
});
```

## Python (pytest)
```python
import pytest
from unittest.mock import Mock, patch

class TestUserService:
    @pytest.fixture
    def service(self, mock_repository):
        return UserService(mock_repository)
    
    @pytest.fixture
    def mock_repository(self):
        return Mock(spec=UserRepository)
    
    def test_get_user_by_id(self, service, mock_repository):
        # Arrange
        user = User(id=123, name="John")
        mock_repository.find_by_id.return_value = user
        
        # Act
        result = service.get_user(123)
        
        # Assert
        assert result == user
        mock_repository.find_by_id.assert_called_once_with(123)
```

## React Component Testing
```typescript
import { render, screen, fireEvent } from '@testing-library/react';

describe('LoginForm', () => {
  it('should submit form with valid credentials', async () => {
    const onSubmit = jest.fn();
    render(<LoginForm onSubmit={onSubmit} />);
    
    fireEvent.change(screen.getByLabelText('Email'), {
      target: { value: 'test@example.com' }
    });
    fireEvent.change(screen.getByLabelText('Password'), {
      target: { value: 'password123' }
    });
    fireEvent.click(screen.getByRole('button', { name: 'Login' }));
    
    expect(onSubmit).toHaveBeenCalledWith({
      email: 'test@example.com',
      password: 'password123'
    });
  });
});
```

## Flutter/Dart Widget Testing
```dart
testWidgets('Counter increments when button is pressed', (tester) async {
  await tester.pumpWidget(const MyApp());
  
  expect(find.text('0'), findsOneWidget);
  expect(find.text('1'), findsNothing);
  
  await tester.tap(find.byIcon(Icons.add));
  await tester.pump();
  
  expect(find.text('0'), findsNothing);
  expect(find.text('1'), findsOneWidget);
});
```

## Best Practices
- Run tests automatically before committing
- Keep tests fast (< 100ms for unit tests)
- Avoid test interdependencies
- Test one thing at a time
- Use test data builders for complex objects
- Clean up after tests (database, files, etc.)
