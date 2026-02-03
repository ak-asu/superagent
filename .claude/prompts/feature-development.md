# Feature Development Prompt

Use this prompt when starting development on a new feature or component.

## Objective
Plan and implement a new feature following best practices for architecture, testing, and documentation.

## Process

### 1. Requirements Analysis
- Clarify functional requirements
- Identify non-functional requirements (performance, security, scalability)
- List assumptions and constraints
- Define success criteria

### 2. Design Phase
- Sketch high-level architecture
- Identify components and their responsibilities
- Define interfaces and contracts
- Plan data models and database schema
- Consider error handling and edge cases

### 3. Implementation Planning
Break down implementation into steps:
- [ ] Set up folder structure
- [ ] Create data models/types
- [ ] Implement core business logic
- [ ] Add API endpoints or UI components
- [ ] Write tests (unit + integration)
- [ ] Add error handling
- [ ] Implement logging and monitoring
- [ ] Update documentation

### 4. Technology Choices
Select appropriate tools:
- **Frontend**: React/Flutter components, state management
- **Backend**: API framework (Express/FastAPI), ORM/query builder
- **Database**: Schema design, indexes, migrations
- **Testing**: Test framework and mocking strategy
- **Infrastructure**: Deployment, monitoring, caching

### 5. Implementation Guidelines

#### Code Structure
```
feature-name/
├── components/          # UI components (if applicable)
├── services/           # Business logic
├── models/             # Data models/types
├── api/                # API endpoints or client
├── utils/              # Helper functions
├── __tests__/          # Test files
└── README.md           # Feature documentation
```

#### Security Checklist
- [ ] Validate all user inputs
- [ ] Use parameterized queries for database
- [ ] Implement proper authentication/authorization
- [ ] Sanitize outputs to prevent XSS
- [ ] No hardcoded secrets
- [ ] Rate limiting for APIs
- [ ] Security headers configured

#### Performance Considerations
- [ ] Database queries optimized (indexes, no N+1)
- [ ] Caching strategy implemented
- [ ] Lazy loading for large data sets
- [ ] Code splitting for frontend
- [ ] Efficient algorithms (check Big O)

#### Testing Strategy
- [ ] Unit tests for business logic (80%+ coverage)
- [ ] Integration tests for API endpoints
- [ ] E2E tests for critical user flows
- [ ] Test error cases and edge cases
- [ ] Mock external dependencies

### 6. Documentation Requirements
- [ ] Function/method documentation (JSDoc/docstrings)
- [ ] API documentation (endpoints, request/response examples)
- [ ] README with setup instructions
- [ ] Architecture decision records (if applicable)
- [ ] Update main project README

### 7. Code Review Checklist
Before submitting:
- [ ] Code follows project conventions
- [ ] All tests passing
- [ ] No linter errors or warnings
- [ ] No console.log or print statements
- [ ] No commented-out code
- [ ] Sensitive data not exposed
- [ ] Error handling implemented
- [ ] Documentation updated

## Example: User Authentication Feature

### Requirements
- Users can register with email/password
- Users can log in and receive JWT token
- Passwords must be hashed
- Rate limiting to prevent brute force
- Session expiration after 1 hour

### Implementation Steps

1. **Data Model**
```typescript
interface User {
  id: string;
  email: string;
  passwordHash: string;
  createdAt: Date;
  lastLoginAt?: Date;
}
```

2. **API Endpoints**
- POST `/api/auth/register` - Create new user
- POST `/api/auth/login` - Authenticate user
- POST `/api/auth/logout` - Invalidate token
- GET `/api/auth/me` - Get current user

3. **Security Implementation**
- Use bcrypt for password hashing
- Generate JWT with expiration
- Implement rate limiting (5 attempts per 15 minutes)
- Validate email format
- Enforce password strength

4. **Testing**
```typescript
describe('Authentication', () => {
  it('should register user with valid credentials');
  it('should reject weak passwords');
  it('should login with correct credentials');
  it('should reject invalid credentials');
  it('should rate limit after 5 failed attempts');
  it('should expire token after 1 hour');
});
```

5. **Monitoring**
- Log authentication attempts
- Track failed login rates
- Monitor token expiration patterns
- Alert on unusual activity

## Output Format

Provide implementation in this structure:
1. **Overview**: Brief description of the feature
2. **Architecture**: Component diagram and data flow
3. **Implementation**: Code with inline comments
4. **Tests**: Comprehensive test suite
5. **Documentation**: API docs and usage examples
6. **Next Steps**: Deployment and monitoring plan
