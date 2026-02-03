---
name: pr-create
description: Create a GitHub pull request with proper description. Use when creating PRs or when asked to submit changes for review.
disable-model-invocation: true
allowed-tools: Bash(git:*), Bash(gh:*)
---

# Create Pull Request

Create a well-documented GitHub pull request.

## 1. Pre-flight Checks
```bash
# Check current branch
git branch --show-current

# Ensure we're not on main/master
# Check for uncommitted changes
git status

# Check if branch is pushed
git log origin/$(git branch --show-current)..HEAD 2>/dev/null
```

## 2. Push Branch (if needed)
```bash
git push -u origin $(git branch --show-current)
```

## 3. Gather Context
```bash
# Get commits since branching from main
git log main..HEAD --oneline

# Get full diff
git diff main...HEAD --stat
```

## 4. Create PR

Use this template:
```bash
gh pr create --title "<type>: <short description>" --body "$(cat <<'EOF'
## Summary
<!-- 1-3 bullet points describing the changes -->
-

## Changes
<!-- List of specific changes made -->
-

## Testing
<!-- How to test these changes -->
- [ ]

## Screenshots
<!-- If UI changes, add before/after screenshots -->

## Related Issues
<!-- Link related issues -->
Fixes #

---
Generated with Claude Code
EOF
)"
```

## PR Title Guidelines
- Use conventional commit format: `feat:`, `fix:`, `docs:`, etc.
- Keep under 72 characters
- Use imperative mood: "Add feature" not "Added feature"

## PR Body Guidelines
- Explain WHY the change is needed
- List all significant changes
- Include testing instructions
- Link related issues/PRs
- Add screenshots for UI changes

## After Creation
- Return the PR URL to the user
- Mention any CI checks to watch
