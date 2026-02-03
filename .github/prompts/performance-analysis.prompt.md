# Performance Analysis

Conduct comprehensive performance analysis to identify bottlenecks and optimization opportunities.

## Instructions

When invoked with `/performance-analysis`, perform detailed performance evaluation:

### 1. Performance Profiling Setup

**Tools to Use**

**Frontend (Web)**
- Chrome DevTools Performance tab
- Lighthouse CI
- WebPageTest
- React DevTools Profiler (for React apps)
- Vue DevTools Performance (for Vue apps)

**Backend (Server)**
- Node.js: `node --inspect`, clinic.js
- Python: cProfile, py-spy, memory_profiler
- Database query analyzers

**Load Testing**
- k6
- Artillery
- Apache JMeter
- Locust (Python)

### 2. Performance Metrics Collection

**Frontend Metrics (Core Web Vitals)**

- **LCP** (Largest Contentful Paint): < 2.5s
- **FID** (First Input Delay): < 100ms
- **CLS** (Cumulative Layout Shift): < 0.1
- **FCP** (First Contentful Paint): < 1.8s
- **TTI** (Time to Interactive): < 3.8s
- **TBT** (Total Blocking Time): < 200ms

**Backend Metrics**
- Response time (p50, p95, p99)
- Throughput (requests/second)
- Error rate
- CPU usage
- Memory usage
- Database query time

**Resource Metrics**
- JavaScript bundle size
- CSS size
- Image sizes
- Total page weight
- Number of HTTP requests

### 3. Analysis Areas

#### A. Frontend Performance

**Bundle Analysis**
```bash
# Analyze JavaScript bundle
npx webpack-bundle-analyzer

# Results should show:
- Total bundle size
- Largest packages
- Duplicate dependencies
- Unused code
```

**Rendering Performance**
- Component render count
- Expensive re-renders
- Layout thrashing
- Paint operations
- JavaScript execution time

**Network Performance**
- Resource loading waterfall
- Critical rendering path
- Resource compression
- HTTP/2 multiplexing
- CDN usage

**Optimization Opportunities**:

1. **Code Splitting**
```typescript
// Before: Everything in one bundle
import HeavyComponent from './HeavyComponent';

// After: Lazy load heavy components
const HeavyComponent = lazy(() => import('./HeavyComponent'));
```

2. **Image Optimization**
```html
<!-- Before -->
<img src="large-image.jpg" />

<!-- After -->
<img 
  src="image-800w.webp"
  srcset="image-400w.webp 400w, image-800w.webp 800w"
  loading="lazy"
  alt="Description"
/>
```

3. **Memoization**
```typescript
// Before: Recalculates on every render
function Component({ data }) {
  const result = expensiveCalculation(data);
  return <div>{result}</div>;
}

// After: Memoized calculation
function Component({ data }) {
  const result = useMemo(
    () => expensiveCalculation(data),
    [data]
  );
  return <div>{result}</div>;
}
```

#### B. Backend Performance

**Database Query Analysis**

```sql
-- Use EXPLAIN ANALYZE to profile queries
EXPLAIN ANALYZE
SELECT u.*, p.* 
FROM users u
LEFT JOIN posts p ON u.id = p.user_id
WHERE u.active = true;

-- Look for:
- Sequential scans (should be index scans)
- High cost values
- Large number of rows examined
```

**N+1 Query Problems**
```typescript
// Before: N+1 queries
const users = await User.findAll();
for (const user of users) {
  user.posts = await Post.findAll({ where: { userId: user.id } });
}

// After: Single query with join
const users = await User.findAll({
  include: [{ model: Post }]
});
```

**API Response Time**
- Identify slow endpoints
- Database query time
- External API call time
- Processing time
- Network latency

**Caching Opportunities**
```typescript
// Add caching layer
const cache = new Redis();

async function getUser(id) {
  // Check cache first
  const cached = await cache.get(`user:${id}`);
  if (cached) return JSON.parse(cached);
  
  // Fetch from database
  const user = await User.findById(id);
  
  // Cache for 1 hour
  await cache.setex(`user:${id}`, 3600, JSON.stringify(user));
  
  return user;
}
```

#### C. Algorithm Optimization

**Time Complexity Analysis**

```typescript
// Before: O(n²) - nested loops
function findDuplicates(arr) {
  const duplicates = [];
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j]) {
        duplicates.push(arr[i]);
      }
    }
  }
  return duplicates;
}

// After: O(n) - using Set
function findDuplicates(arr) {
  const seen = new Set();
  const duplicates = new Set();
  
  for (const item of arr) {
    if (seen.has(item)) {
      duplicates.add(item);
    }
    seen.add(item);
  }
  
  return Array.from(duplicates);
}
```

**Data Structure Selection**
- Use Map/Object for lookups instead of Array.find()
- Use Set for uniqueness instead of Array.includes()
- Use appropriate data structures for the use case

#### D. Memory Analysis

**Memory Leaks**
- Event listeners not cleaned up
- Closures holding references
- Global variables accumulation
- Cached data not evicted
- Detached DOM nodes

**Memory Optimization**
```typescript
// Before: Memory leak
useEffect(() => {
  window.addEventListener('resize', handleResize);
}, []);

// After: Cleanup
useEffect(() => {
  window.addEventListener('resize', handleResize);
  return () => window.removeEventListener('resize', handleResize);
}, []);
```

### 4. Performance Report Template

#### Executive Summary
- Current performance status
- Key metrics vs targets
- Critical issues found
- Expected impact of optimizations

#### Detailed Findings

**Finding 1: [Issue Name]**
- **Severity**: Critical / High / Medium / Low
- **Category**: Frontend / Backend / Database / Network
- **Metric Impact**: +2.5s to LCP, -30% throughput
- **Root Cause**: Detailed explanation
- **Current Measurement**: Specific numbers
- **Target Measurement**: Performance goal
- **Recommendation**: Specific solution
- **Implementation Effort**: Hours/days estimate
- **Expected Improvement**: Quantified benefit

#### Optimization Priorities

**Quick Wins** (< 1 day, high impact)
1. Enable gzip compression → -60% transfer size
2. Add database index on frequently queried column → -80% query time
3. Lazy load below-the-fold images → -40% initial page load

**Medium-term** (1-5 days)
1. Implement Redis caching → -50% database load
2. Code splitting for routes → -40% initial bundle size
3. Optimize images (WebP, responsive) → -50% image bytes

**Long-term** (1-2 weeks)
1. Migrate to React 18 with concurrent features
2. Implement virtual scrolling for lists
3. Refactor expensive algorithms

### 5. Load Testing Results

**Test Scenario**: [Description]
**Duration**: X minutes
**Virtual Users**: Y concurrent users
**RPS Target**: Z requests/second

**Results**:
```
Average Response Time: 250ms (target: < 200ms) ⚠️
95th Percentile: 800ms (target: < 500ms) ❌
Error Rate: 0.1% (target: < 0.1%) ✅
Throughput: 450 RPS (target: 500 RPS) ⚠️
```

**Bottlenecks Identified**:
1. Database connection pool exhausted at 80 concurrent users
2. Memory usage spikes at 400 RPS
3. CPU usage reaches 90% during peak load

### 6. Monitoring Setup

**Recommended Tools**
- APM: New Relic, Datadog, AppDynamics
- Error Tracking: Sentry, Rollbar
- Real User Monitoring (RUM)
- Synthetic monitoring

**Alerts to Configure**
- Response time > threshold
- Error rate > threshold
- Resource utilization > threshold
- Core Web Vitals degradation

### 7. Before/After Comparison

Present optimizations with clear metrics:

```
Metric                Before    After     Improvement
────────────────────────────────────────────────────
LCP                   4.2s      1.8s      -57%
Bundle Size           450KB     180KB     -60%
API Response (p95)    850ms     320ms     -62%
Database Queries      15/req    3/req     -80%
Memory Usage          1.2GB     450MB     -62%
```

### 8. Action Items

Prioritized list of optimizations:

**Priority 1 (Critical - Do Now)**
- [ ] Add missing database indexes
- [ ] Enable response compression
- [ ] Fix memory leak in WebSocket handler

**Priority 2 (High - This Sprint)**
- [ ] Implement caching layer
- [ ] Optimize expensive queries
- [ ] Code split large bundles

**Priority 3 (Medium - Next Sprint)**
- [ ] Lazy load images
- [ ] Optimize render performance
- [ ] Implement virtual scrolling

**Priority 4 (Low - Backlog)**
- [ ] Migrate to newer framework version
- [ ] Refactor legacy code
- [ ] Additional monitoring

## Usage

Run performance analysis:
```
/performance-analysis
```

Focus on specific areas:
```
/performance-analysis focus on frontend
/performance-analysis analyze database queries
/performance-analysis review bundle size
/performance-analysis check memory usage
```
