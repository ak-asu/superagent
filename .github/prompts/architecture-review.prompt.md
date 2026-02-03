# Architecture Review

Conduct a comprehensive architecture review of the system design, identifying strengths, weaknesses, and improvement opportunities.

## Instructions

When invoked with `/architecture-review`, perform a thorough architectural analysis:

### 1. System Overview

**Current Architecture**
- Architectural style (monolithic, microservices, serverless, etc.)
- Major components and their responsibilities
- Technology stack
- Integration points
- Deployment architecture

**Context**
- Business requirements driving the design
- Scale and performance needs
- Team size and expertise
- Budget and timeline constraints

### 2. Architecture Evaluation Framework

#### A. Design Principles Assessment

**SOLID Principles**
- ✅/❌ Single Responsibility: Components have focused purposes
- ✅/❌ Open/Closed: Extensible without modification
- ✅/❌ Liskov Substitution: Proper inheritance/interface usage
- ✅/❌ Interface Segregation: Focused interfaces
- ✅/❌ Dependency Inversion: Depend on abstractions

**DRY (Don't Repeat Yourself)**
- ✅/❌ Code duplication minimized
- ✅/❌ Shared libraries for common functionality
- ✅/❌ Configuration centralization

**Separation of Concerns**
- ✅/❌ Clear boundaries between layers
- ✅/❌ Business logic separated from infrastructure
- ✅/❌ Presentation layer isolated

#### B. Quality Attributes (Non-Functional Requirements)

**Scalability**
- Horizontal scaling capability
- Load balancing strategy
- Database scaling approach
- Caching implementation
- Rate limiting and throttling

**Performance**
- Response time targets
- Throughput capacity
- Resource utilization
- Optimization opportunities

**Reliability**
- Fault tolerance mechanisms
- Error handling strategy
- Retry and circuit breaker patterns
- Monitoring and alerting

**Security**
- Authentication and authorization
- Data encryption (at rest and in transit)
- API security
- Secrets management
- Compliance requirements (GDPR, HIPAA, etc.)

**Maintainability**
- Code organization and modularity
- Documentation quality
- Testing coverage
- Deployment automation
- Technical debt level

**Availability**
- Uptime targets (SLA)
- Redundancy and failover
- Disaster recovery plan
- Backup strategy

### 3. Component Analysis

For each major component, evaluate:

**Responsibilities**
- Clear single purpose?
- Appropriate size and complexity?
- Well-defined boundaries?

**Dependencies**
- Coupling level (tight vs loose)
- Dependency direction correct?
- Circular dependencies?

**Communication**
- Synchronous vs asynchronous
- Protocol choices (REST, gRPC, events)
- Error handling and retries

### 4. Data Architecture Review

**Data Model**
- Schema design appropriateness
- Normalization vs denormalization choices
- Indexing strategy
- Data consistency approach

**Data Flow**
- How data moves through the system
- Transformation points
- Validation strategy
- Data integrity measures

**Storage Decisions**
- Database choices justified?
- Caching strategy effective?
- Data partitioning/sharding needs

### 5. Integration Architecture

**External Integrations**
- Third-party service dependencies
- API contracts and versioning
- Integration patterns used
- Failure handling for external services

**Internal Communication**
- Service-to-service communication
- Event-driven patterns
- Message queues and topics
- API gateway usage

### 6. Identified Issues

For each issue, document:

**Severity**: Critical / High / Medium / Low

**Category**: Performance / Security / Scalability / Maintainability / etc.

**Description**: Clear explanation of the problem

**Impact**: Business and technical consequences

**Current Risk**: What could go wrong

**Recommendation**: Specific solution with tradeoffs

**Example**:
```
Severity: High
Category: Scalability
Description: Database queries are not optimized, causing N+1 query problems
Impact: Response times degrade under load, poor user experience
Current Risk: System cannot handle peak traffic
Recommendation: Implement query optimization and caching layer
  - Use eager loading for relationships
  - Add Redis caching for frequently accessed data
  - Consider read replicas for query load distribution
Tradeoff: Added complexity, eventual consistency with cache
```

### 7. Architectural Strengths

Highlight what's working well:
- Design patterns used effectively
- Good separation of concerns
- Appropriate technology choices
- Scalability provisions
- Security measures
- Code quality

### 8. Improvement Roadmap

**Quick Wins** (< 1 week)
- Low effort, high impact improvements
- Critical bug fixes
- Simple optimizations

**Short-term** (1-4 weeks)
- Medium complexity improvements
- Technical debt reduction
- Performance optimizations

**Long-term** (1-3 months)
- Architectural refactoring
- Major technology migrations
- Infrastructure improvements

**Strategic** (3+ months)
- Platform evolution
- Complete redesigns if needed
- Major capability additions

### 9. Alternative Architectures

Consider alternative approaches:

**Option A: [Alternative approach]**
- Pros: Benefits and advantages
- Cons: Drawbacks and challenges
- Migration effort: Estimated complexity
- When to consider: Appropriate scenarios

### 10. Decision Records (ADRs)

Document key architectural decisions:

**Decision**: What was decided
**Context**: Why the decision was needed
**Alternatives Considered**: Other options evaluated
**Consequences**: Positive and negative outcomes
**Status**: Accepted / Superseded / Deprecated

## Output Format

Provide a structured report with:
1. Executive Summary (1 page)
2. Detailed Analysis (by section above)
3. Risk Matrix (severity vs likelihood)
4. Prioritized Recommendations
5. Implementation Roadmap

## Usage

Select the codebase/design documents and run:
```
/architecture-review
```

Optionally specify focus area:
```
/architecture-review focus on scalability
/architecture-review focus on security
/architecture-review for microservices migration
```
