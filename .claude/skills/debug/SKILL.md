---
name: debug
description: Debug and fix issues in code. Use when troubleshooting bugs, errors, or unexpected behavior.
---

# Debug Assistant

Systematic approach to debugging issues.

## 1. Understand the Problem
- What is the expected behavior?
- What is the actual behavior?
- When did it start happening?
- Is it reproducible? Under what conditions?

## 2. Gather Information
- Read error messages carefully
- Check logs for stack traces
- Identify the last known working state
- Look for recent changes

## 3. Reproduce the Issue
- Create minimal reproduction steps
- Isolate the failing component
- Document exact inputs that cause the issue

## 4. Form Hypotheses
Based on the symptoms, list possible causes:
1. Most likely: ...
2. Second possibility: ...
3. Less likely but possible: ...

## 5. Investigate Systematically

### For Runtime Errors
- Check for null/undefined values
- Verify data types and formats
- Check array bounds and object keys
- Verify async/await handling

### For Logic Errors
- Add logging at key points
- Check conditional logic
- Verify loop bounds and exit conditions
- Trace data flow

### For Performance Issues
- Profile the code
- Check for O(n^2) or worse algorithms
- Look for memory leaks
- Check for unnecessary re-renders (React)

## 6. Fix and Verify
- Make the minimal change to fix the issue
- Add tests to prevent regression
- Verify the fix doesn't break other things
- Document the root cause

## Output Format
```
## Problem
[Clear description of the issue]

## Root Cause
[What was actually wrong]

## Solution
[The fix applied]

## Prevention
[How to prevent similar issues]
```
