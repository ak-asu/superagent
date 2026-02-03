---
name: commit
description: Create a well-formatted git commit with conventional commit message. Use when committing changes to git.
disable-model-invocation: true
allowed-tools: Bash(git:*)
---

# Git Commit

Create a git commit following these steps:

## 1. Analyze Changes
First, check what has changed:
- Run `git status` to see modified files
- Run `git diff --staged` to see staged changes
- If nothing staged, run `git diff` to see unstaged changes

## 2. Stage Changes
If not already staged, stage the relevant files:
- Use `git add <specific-files>` for targeted commits
- Avoid `git add .` unless all changes are related

## 3. Determine Commit Type
Use conventional commits format:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style (formatting, semicolons, etc.)
- `refactor`: Code restructuring without behavior change
- `perf`: Performance improvement
- `test`: Adding or updating tests
- `chore`: Maintenance tasks, dependencies
- `ci`: CI/CD changes
- `build`: Build system changes

## 4. Write Commit Message

Format:
```
<type>(<scope>): <short description>

<optional body explaining why, not what>

<optional footer with breaking changes or issue refs>
```

Guidelines:
- Subject line: max 50 characters, imperative mood
- Body: wrap at 72 characters
- Explain "why" not "what" (the diff shows what)
- Reference issues: "Fixes #123" or "Relates to #456"

## 5. Create Commit
```bash
git commit -m "$(cat <<'EOF'
<type>(<scope>): <description>

<body>

Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"
```

## Do NOT
- Push to remote (unless explicitly asked)
- Use `--amend` (unless explicitly asked)
- Use `--no-verify` (unless explicitly asked)
