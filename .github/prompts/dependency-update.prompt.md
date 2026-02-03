# Dependency Update Assistant

Help safely update project dependencies, identifying breaking changes and required code modifications.

## Instructions

When invoked with `/dependency-update`, assist with dependency management:

### 1. Analyze Current Dependencies

**Scan Project Files**
- `package.json` / `package-lock.json` (Node.js)
- `requirements.txt` / `Pipfile` / `pyproject.toml` (Python)
- `pubspec.yaml` (Flutter/Dart)
- `Gemfile` (Ruby)
- `pom.xml` / `build.gradle` (Java)

**Identify Outdated Dependencies**
```bash
# For each dependency, show:
Package: react
Current: 17.0.2
Latest: 18.2.0
Type: major update
```

### 2. Categorize Updates

**Security Updates** (Critical Priority)
- CVE vulnerabilities
- Security advisories
- Immediate action required

**Major Updates** (Breaking Changes)
- Semver major version changes
- Requires code modifications
- Test thoroughly before deploying

**Minor Updates** (New Features)
- Backward compatible
- New features added
- Low risk

**Patch Updates** (Bug Fixes)
- Bug fixes only
- Minimal risk
- Can usually be auto-applied

### 3. Breaking Change Analysis

For each major update:

**Package**: `[package-name]`
**Version**: `[old] → [new]`

**Breaking Changes**:
1. API method renamed: `oldMethod()` → `newMethod()`
2. Configuration format changed
3. Deprecated feature removed
4. New peer dependency required

**Migration Guide**:
```typescript
// Before
import { oldAPI } from 'package';
oldAPI.doSomething();

// After
import { newAPI } from 'package';
newAPI.doSomething({ newOption: true });
```

**Files Affected**:
- `src/components/Feature.tsx`
- `src/utils/helper.ts`
- `tests/integration.test.ts`

### 4. Dependency Tree Analysis

**Check for Conflicts**
- Peer dependency mismatches
- Transitive dependency issues
- Version conflicts between packages

**Example**:
```
⚠️ Peer dependency conflict detected:
  react-router-dom@6.x requires react@^18.0.0
  but you have react@17.0.2 installed
  
Resolution: Update react to ^18.0.0 first
```

### 5. Update Strategy

**Strategy A: Incremental Updates**
- Update one major package at a time
- Test thoroughly after each update
- Safest approach for complex projects

**Strategy B: Batch Minor/Patch Updates**
- Group low-risk updates together
- Update all at once
- Faster for maintenance updates

**Strategy C: Fresh Install**
- Delete lock file
- Reinstall all dependencies
- Resolve conflicts clean

### 6. Testing Checklist

Before updating:
- [ ] Create feature branch
- [ ] Run full test suite (baseline)
- [ ] Document current behavior
- [ ] Back up working version

After updating each package:
- [ ] Install new version
- [ ] Fix TypeScript/compilation errors
- [ ] Run unit tests
- [ ] Run integration tests
- [ ] Manual testing of affected features
- [ ] Check for console warnings/errors
- [ ] Review bundle size changes
- [ ] Performance testing if needed

### 7. Update Commands

**Node.js/npm**
```bash
# Check for outdated packages
npm outdated

# Update specific package
npm install package@latest

# Update all to latest
npm update

# Check for security vulnerabilities
npm audit
npm audit fix
```

**Python/pip**
```bash
# Check outdated
pip list --outdated

# Update specific package
pip install --upgrade package-name

# Update all in requirements.txt
pip install --upgrade -r requirements.txt

# Check for security issues
pip-audit
```

**Flutter/Dart**
```bash
# Check for outdated packages
flutter pub outdated

# Update packages
flutter pub upgrade

# Get latest versions
flutter pub upgrade --major-versions
```

### 8. Changelog Review

For each major update, review:

**Official Changelog**
- New features
- Breaking changes
- Deprecations
- Bug fixes
- Migration guides

**Key Resources**
- Official migration guides
- GitHub release notes
- Community discussions
- Known issues

### 9. Risk Assessment

For each update, evaluate:

**Impact**: High / Medium / Low
**Risk**: High / Medium / Low
**Effort**: High / Medium / Low

**Example**:
```
Package: react (17.0.2 → 18.2.0)
Impact: High (core framework)
Risk: Medium (well-documented migration)
Effort: Medium (API changes required)
Priority: High
Recommendation: Schedule dedicated sprint
```

### 10. Rollback Plan

**If Update Fails**:
1. Revert to previous commit
2. Restore package-lock.json/yarn.lock
3. Run `npm ci` / `yarn install --frozen-lockfile`
4. Document issues encountered
5. Create issue for future attempt

### 11. Post-Update Verification

**Automated Checks**
- All tests pass
- No TypeScript errors
- Linting passes
- Build succeeds
- Bundle size acceptable

**Manual Checks**
- App starts successfully
- Critical features work
- No console errors
- Performance acceptable
- UI renders correctly

**Monitoring**
- Watch error tracking (Sentry, etc.)
- Monitor performance metrics
- Check user reports
- Review server logs

### 12. Documentation Updates

After successful update:
- [ ] Update package.json
- [ ] Update README if needed
- [ ] Update CI/CD if needed
- [ ] Document breaking changes
- [ ] Update team wiki
- [ ] Notify team members

## Update Priority Matrix

| Priority | Type | Example | Timeline |
|----------|------|---------|----------|
| 🔴 Critical | Security vulnerability | CVE with exploit | Immediately |
| 🟠 High | Major framework update | React 17→18 | Next sprint |
| 🟡 Medium | Minor update | New features | This quarter |
| 🟢 Low | Patch update | Bug fixes | Routine maintenance |

## Usage

Run dependency update check:
```
/dependency-update
```

Focus on specific areas:
```
/dependency-update check security vulnerabilities
/dependency-update plan React upgrade
/dependency-update review breaking changes in package-name
```
