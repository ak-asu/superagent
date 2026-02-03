# Code Migration Assistant

Help migrate code from one framework/version to another, ensuring all breaking changes are addressed.

## Instructions

When invoked with `/migration`, assist with code migration by:

### 1. Analyze Current Code
- Identify current framework/library versions
- List dependencies that need updating
- Detect deprecated APIs and patterns
- Find breaking changes in target version

### 2. Create Migration Plan

**Scope**
- What needs to be migrated
- Estimated effort and risk level
- Order of operations

**Breaking Changes**
- List all breaking changes between versions
- Impact assessment for each change
- Mitigation strategies

**Dependencies**
- Updated dependency versions
- New peer dependencies
- Removed dependencies

### 3. Step-by-Step Migration Guide

For each component/module:

**Step 1: Update Dependencies**
```json
// Before
"react": "^17.0.2"

// After
"react": "^18.2.0"
```

**Step 2: Code Changes**
```typescript
// Before (deprecated)
import { render } from 'react-dom';
render(<App />, document.getElementById('root'));

// After (new API)
import { createRoot } from 'react-dom/client';
const root = createRoot(document.getElementById('root'));
root.render(<App />);
```

**Step 3: Test & Verify**
- Run test suite
- Check for console warnings
- Verify functionality

### 4. Common Migration Scenarios

**React 17 → React 18**
- Update render API
- Handle automatic batching changes
- Update useEffect cleanup
- Address Suspense changes
- Update TypeScript types

**Node.js Version Upgrades**
- Update async_hooks usage
- Handle deprecated APIs
- Update package.json engines field
- Address breaking changes in core modules

**Python 2 → Python 3**
- Convert print statements to functions
- Update division operator behavior
- Handle string/bytes changes
- Update exception syntax
- Convert iteritems() to items()

**Vue 2 → Vue 3**
- Update component lifecycle hooks
- Convert Vue.set to reactive()
- Update event emitters
- Address filters removal
- Update v-model syntax

**Angular Upgrades**
- Run ng update commands
- Update decorators
- Handle HttpClient changes
- Update router syntax
- Address dependency injection changes

### 5. Testing Strategy

**Before Migration**
- Create comprehensive test suite
- Document current behavior
- Capture baseline metrics

**During Migration**
- Incremental testing
- Feature flag rollout
- A/B testing if possible

**After Migration**
- Full regression testing
- Performance comparison
- Monitor error rates

### 6. Risk Mitigation

**Rollback Plan**
- Version control checkpoints
- Feature toggles
- Deployment rollback procedure

**Gradual Rollout**
- Canary deployments
- Phased migration
- Parallel running (if feasible)

### 7. Documentation Updates

After migration, update:
- README with new setup instructions
- Dependency documentation
- API documentation for changed endpoints
- Team wiki/confluence pages
- Migration notes for future reference

## Migration Checklist

- [ ] Backup current working version
- [ ] Update dependencies in package.json/requirements.txt
- [ ] Address breaking changes
- [ ] Update deprecated APIs
- [ ] Run and fix tests
- [ ] Update TypeScript types (if applicable)
- [ ] Clear build caches
- [ ] Update CI/CD pipelines
- [ ] Update documentation
- [ ] Deploy to staging
- [ ] Conduct thorough testing
- [ ] Monitor for issues
- [ ] Document lessons learned

## Usage

Specify the migration:
```
/migration migrate from React 17 to React 18
/migration upgrade Python from 3.8 to 3.11
/migration convert JavaScript to TypeScript
/migration migrate from REST API to GraphQL
```
