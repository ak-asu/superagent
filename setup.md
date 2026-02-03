# VS Code + Agent Skills Setup Guide

This consolidated document merges the workspace's `SETUP-GUIDE.md` and `AGENT-SKILLS-SETUP.md` into a single reference file. It preserves all information from both original files.

---

# VS Code + GitHub Copilot + Claude Code Configuration Guide

This document explains all the configurations created in this workspace and how to use them effectively.

---

## Directory Structure

```
your-project/
├── .claude/
│   ├── settings.json          # Claude Code permissions & settings
│   └── skills/                # Custom Claude Code skills
│       ├── code-review/
│       ├── commit/
│       ├── debug/
│       ├── document/
│       ├── explain-code/
│       ├── pr-create/
│       ├── refactor/
│       └── test-generator/
├── .github/
│   └── copilot-instructions.md # GitHub Copilot custom instructions
├── .vscode/
│   ├── settings.json          # VS Code + Copilot settings
│   └── mcp.json               # MCP servers for VS Code Copilot
├── .mcp.json                  # MCP servers for Claude Code
├── CLAUDE.md                  # Claude Code memory/context file
└── SETUP-GUIDE.md            # This file
```

---

## 1. Claude Code Configuration

### CLAUDE.md - Memory File
**Location**: `CLAUDE.md` (project root) or `~/.claude/CLAUDE.md` (global)

This file is automatically loaded at the start of every Claude Code session. Use it for:
- Personal preferences and coding style
- Project-specific context
- Common instructions you want Claude to follow

### .claude/settings.json - Permissions
**Location**: `.claude/settings.json`

Controls what Claude Code can do automatically without asking permission:

```json
{
  "permissions": {
    "allow": ["Bash(npm:*)", "Bash(git:*)"],  // Auto-approved
    "deny": ["Read(.env)"]                     // Always blocked
  }
}
```

### Skills - Custom Slash Commands
**Location**: `.claude/skills/<skill-name>/SKILL.md`

Skills are reusable instructions invoked with `/skill-name`:

| Skill | Command | Description |
|-------|---------|-------------|
| Code Review | `/code-review` | Comprehensive code review |
| Commit | `/commit` | Create conventional git commit |
| Debug | `/debug` | Systematic debugging assistance |
| Document | `/document` | Generate JSDoc/docstrings |
| Explain Code | `/explain-code` | Explain code with diagrams |
| PR Create | `/pr-create` | Create GitHub pull request |
| Refactor | `/refactor` | Improve code quality |
| Test Generator | `/test-generator` | Generate unit tests |

**Usage in Claude Code:**
```
/code-review src/components/Button.tsx
/commit
/test-generator src/utils/helpers.ts
```

---

## 2. GitHub Copilot Configuration

### .github/copilot-instructions.md
**Location**: `.github/copilot-instructions.md`

Global instructions that Copilot follows for all suggestions:
- Code style preferences
- Naming conventions
- Error handling patterns
- Security practices

**Enable in VS Code settings:**
```json
"github.copilot.chat.codeGeneration.useInstructionFiles": true
```

### Path-Specific Instructions
**Location**: `.github/instructions/<name>.instructions.md`

Create targeted instructions for specific parts of your codebase:

```
.github/instructions/
├── frontend.instructions.md    # React-specific patterns
├── backend.instructions.md     # API-specific patterns
└── tests.instructions.md       # Testing conventions
```

Example `frontend.instructions.md`:
```markdown
---
applyTo: "src/components/**"
---
# Frontend Component Guidelines
- Use functional components with hooks
- Extract logic into custom hooks
- Use Tailwind for styling
```

---

## 3. MCP Server Configuration

### For Claude Code: .mcp.json
**Location**: `.mcp.json` (project root)

```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "@package/name"],
      "env": {}
    }
  }
}
```

### For VS Code Copilot: .vscode/mcp.json
**Location**: `.vscode/mcp.json`

Same format, but for Copilot's MCP integration.

### Popular MCP Servers to Add

| Server | Purpose | Install Command |
|--------|---------|-----------------|
| Filesystem | File operations | `claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem .` |
| Memory | Persistent memory | `claude mcp add memory -- npx -y @modelcontextprotocol/server-memory` |
| GitHub | GitHub API access | `claude mcp add github --env GITHUB_TOKEN=xxx -- npx -y @modelcontextprotocol/server-github` |
| PostgreSQL | Database queries | `claude mcp add postgres -- npx -y @modelcontextprotocol/server-postgres` |
| Notion | Notion API | `claude mcp add --transport http notion https://mcp.notion.com/mcp` |
| Sentry | Error monitoring | `claude mcp add --transport http sentry https://mcp.sentry.dev/mcp` |

**Add servers via CLI:**
```bash
# HTTP/SSE (remote) servers
claude mcp add --transport http <name> <url>

# Stdio (local) servers
claude mcp add --transport stdio <name> -- <command>

# List configured servers
claude mcp list

# Check server status in Claude Code
/mcp
```

---

## 4. VS Code Settings

### .vscode/settings.json

Key Copilot settings configured:

```json
{
  // Enable Copilot everywhere
  "github.copilot.enable": { "*": true },

  // Use instruction files
  "github.copilot.chat.codeGeneration.useInstructionFiles": true,

  // Enable inline suggestions
  "editor.inlineSuggest.enabled": true,

  // Workspace indexing for better context
  "github.copilot.chat.indexing.enabled": true
}
```

---

## 5. Usage Tips

### Claude Code Skills
```bash
# In Claude Code terminal:
/code-review              # Review current file
/commit                   # Stage and commit changes
/test-generator utils.ts  # Generate tests for file
/explain-code             # Explain selected code
```

### Copilot Chat Participants
```
@workspace  # Ask about entire project
@terminal   # Terminal help
@vscode     # VS Code settings help
#file       # Reference specific file
#selection  # Reference selected code
```

### Copilot Slash Commands
```
/doc        # Generate documentation
/explain    # Explain code
/fix        # Fix errors
/test       # Generate tests
/optimize   # Suggest optimizations
```

### Context References
```
#file:src/app.ts          # Reference file
#codebase                 # Search entire codebase
@workspace                # Full workspace context
```

---

## 6. Recommended Extensions

### Essential
- **GitHub Copilot** - AI pair programmer
- **GitHub Copilot Chat** - Conversational AI
- **Claude Code** - Anthropic's CLI in VS Code

### Productivity
- **GitLens** - Git supercharged
- **Error Lens** - Inline error display
- **Prettier** - Code formatting
- **ESLint** - JavaScript linting

### Language-Specific
- **Dart** - Flutter/Dart support
- **Python** - Python language support
- **Pylance** - Python IntelliSense

---

## 7. Installation Checklist

- [ ] Copy `.claude/` folder to project root
- [ ] Copy `.github/` folder to project root
- [ ] Copy `.vscode/` folder to project root
- [ ] Copy `CLAUDE.md` to project root
- [ ] Copy `.mcp.json` to project root (optional)
- [ ] Customize `copilot-instructions.md` for your project
- [ ] Customize `CLAUDE.md` for your preferences
- [ ] Add MCP servers as needed
- [ ] Restart VS Code to apply settings

---

## 8. Quick Reference

### Claude Code Commands
| Command | Description |
|---------|-------------|
| `/help` | Show all commands |
| `/mcp` | Manage MCP servers |
| `/compact` | Reduce context size |
| `/clear` | Clear conversation |
| `/init` | Initialize CLAUDE.md |

### File Locations
| File | Scope | Purpose |
|------|-------|---------|
| `CLAUDE.md` | Project | Claude context |
| `~/.claude/CLAUDE.md` | Global | Global Claude context |
| `.claude/settings.json` | Project | Claude permissions |
| `~/.claude/settings.json` | Global | Global permissions |
| `.github/copilot-instructions.md` | Project | Copilot instructions |
| `.vscode/settings.json` | Project | VS Code settings |
| `.mcp.json` | Project | MCP servers (Claude) |
| `.vscode/mcp.json` | Project | MCP servers (Copilot) |

---

## Resources

- [Claude Code Docs](https://code.claude.com/docs)
- [GitHub Copilot Docs](https://docs.github.com/copilot)
- [MCP Protocol](https://modelcontextprotocol.io)
- [Agent Skills Spec](https://agentskills.io/specification)
- [Skills Directory](https://skills.sh)

---

# Agent Skills Setup Guide

This guide explains how to set up portable Agent Skills that work across VS Code, Copilot CLI, and the Copilot coding agent.

## What are Agent Skills?

Agent Skills are reusable, portable AI capabilities defined using an open standard. Unlike custom instructions (always active) or Claude skills (tool-specific), Agent Skills:

- Load on-demand when contextually relevant
- Work across multiple tools (VS Code, CLI, coding agent)
- Reduce token consumption by loading only when needed
- Enable skill composition for complex workflows
- Support team collaboration via version control

## Directory Structure

**Personal Skills** (recommended):
```
~/.copilot/skills/
├── test-generator/
│   ├── skill.yaml
│   ├── instructions.md
│   ├── examples/
│   └── resources/
├── refactor/
├── debug/
└── code-review/
```

**Project Skills** (team-shared):
```
.github/skills/
├── api-design/
├── deployment/
└── database-migration/
```

## Skill Structure

Each skill is a directory containing:

### 1. skill.yaml (Required)

Metadata for skill discovery and activation:

```yaml
name: test-generator
version: 1.0.0
description: Generate comprehensive unit tests with edge case coverage
author: Your Team
tags:
  - testing
  - unit-tests
  - tdd

# Context matching - when to load this skill
triggers:
  keywords:
    - "test"
    - "unit test"
    - "generate tests"
  file_patterns:
    - "**/*.test.ts"
    - "**/*.spec.ts"
    - "**/test/**"
  commands:
    - "test"
    - "generate-tests"

# Supported programming languages
languages:
  - typescript
  - javascript
  - python
  - dart

# Dependencies (other skills this depends on)
dependencies: []
```

### 2. instructions.md (Required)

Core skill instructions:

```markdown
# Test Generator

Generate comprehensive unit tests following best practices.

## When to Use

Use this skill when:
- Writing tests for new functions
- Adding missing test coverage
- Refactoring existing tests

## Instructions

Generate tests that:

1. Follow AAA pattern (Arrange-Act-Assert)
2. Use descriptive names: `should [behavior] when [condition]`
3. Cover happy path and error cases
4. Include edge cases and boundary conditions
5. Mock external dependencies

## Test Structure

```typescript
describe('FunctionName', () => {
  // Setup
  beforeEach(() => {
    // Initialize dependencies
  });
  
  it('should return expected result when input is valid', () => {
    // Arrange
    const input = createTestData();
    
    // Act
    const result = functionUnderTest(input);
    
    // Assert
    expect(result).toBe(expectedValue);
  });
  
  it('should throw error when input is invalid', () => {
    expect(() => functionUnderTest(null)).toThrow(ValidationError);
  });
});
```

## Framework-Specific Patterns

### Jest/Vitest (TypeScript/JavaScript)
- Use `describe()` for grouping
- Use `it()` or `test()` for test cases
- Mock with `jest.fn()` or `vi.fn()`

### pytest (Python)
- Use `test_` prefix for functions
- Use fixtures for setup
- Use `pytest.raises()` for exceptions

### flutter_test (Dart)
- Use `testWidgets()` for widget tests
- Use `test()` for unit tests
- Use `setUp()` for initialization
```

### 3. examples/ (Optional)

Example implementations:

```
examples/
├── typescript-jest.md
├── python-pytest.md
└── dart-flutter.md
```

**typescript-jest.md:**
```markdown
# TypeScript + Jest Example

## Input Code
```typescript
function calculateDiscount(price: number, percentage: number): number {
  if (price < 0 || percentage < 0 || percentage > 100) {
    throw new Error('Invalid input');
  }
  return price * (percentage / 100);
}
```

## Generated Tests
```typescript
describe('calculateDiscount', () => {
  it('should calculate discount correctly', () => {
    expect(calculateDiscount(100, 10)).toBe(10);
    expect(calculateDiscount(50, 20)).toBe(10);
  });
  
  it('should handle zero percentage', () => {
    expect(calculateDiscount(100, 0)).toBe(0);
  });
  
  it('should throw error for negative price', () => {
    expect(() => calculateDiscount(-10, 10)).toThrow('Invalid input');
  });
  
  it('should throw error for percentage over 100', () => {
    expect(() => calculateDiscount(100, 150)).toThrow('Invalid input');
  });
});
```
```

### 4. resources/ (Optional)

Supporting files:

```
resources/
├── templates/
│   ├── jest.template.ts
│   └── pytest.template.py
├── patterns/
│   └── common-mocks.md
└── references/
    └── testing-best-practices.md
```

## Creating a Skill from Claude Skills

### Example: Migrating "code-review" skill

**1. Create directory structure:**
```bash
mkdir -p ~/.copilot/skills/code-review/examples
mkdir -p ~/.copilot/skills/code-review/resources
```

**2. Create skill.yaml:**
```yaml
name: code-review
version: 1.0.0
description: Perform comprehensive code review for quality, security, and performance
author: MG
tags:
  - code-review
  - quality
  - security
  - best-practices

triggers:
  keywords:
    - "review"
    - "code review"
    - "check code"
  commands:
    - "review"
    - "code-review"

languages:
  - typescript
  - javascript
  - python
  - dart

dependencies: []
```

**3. Copy existing SKILL.md to instructions.md:**
```bash
cp .claude/skills/code-review/SKILL.md ~/.copilot/skills/code-review/instructions.md
```

**4. Add examples (optional but recommended):**

Create `examples/security-review.md`:
```markdown
# Security Review Example

## Code with Issues
```typescript
app.post('/api/users', (req, res) => {
  const { username, password } = req.body;
  db.query(`INSERT INTO users VALUES ('${username}', '${password}')`);
  res.json({ success: true });
});
```

## Review Output

**Location**: api/routes/users.ts:15

**Severity**: Critical

**Issue**: SQL Injection Vulnerability

**Description**: User input is directly interpolated into SQL query without sanitization.

**Suggestion**: Use parameterized queries
```typescript
const query = 'INSERT INTO users (username, password) VALUES (?, ?)';
db.query(query, [username, hashedPassword]);
```
```

## Skills to Create

### Priority Skills

1. **test-generator** - Generate comprehensive tests
2. **refactor** - Code improvement suggestions
3. **debug** - Systematic debugging assistance
4. **security-audit** - Security vulnerability detection
5. **performance-optimize** - Performance bottleneck identification
6. **api-design** - REST/GraphQL API design guidance
7. **database-optimize** - Query and schema optimization

### Skill Templates

Each skill should include:
- Clear triggers (when to activate)
- Language-specific instructions
- Examples for common scenarios
- Best practices and anti-patterns
- Framework-specific guidance

## Using Agent Skills

### In VS Code

Skills load automatically when context matches:
```
User: "Generate tests for this function"
→ test-generator skill loads automatically
```

### In Copilot CLI

```bash
copilot "review this code for security issues"
→ security-audit skill loads automatically
```

### Manual Invocation

```bash
# List available skills
copilot --list-skills

# Use specific skill
copilot --skill=test-generator "generate tests for calculateDiscount()"
```

## Skill Composition

Combine multiple skills for complex workflows:

```yaml
# deployment-checklist.yaml
name: deployment-checklist
dependencies:
  - test-generator  # Ensure tests exist
  - security-audit  # Check for vulnerabilities
  - performance-optimize  # Verify performance
```

## Best Practices

### Skill Design
- Keep skills focused on single capabilities
- Use clear, specific triggers
- Provide language-specific guidance
- Include real-world examples
- Document edge cases

### Maintenance
- Version skills semantically (1.0.0, 1.1.0, 2.0.0)
- Document breaking changes
- Keep examples up-to-date
- Test skills regularly

### Team Collaboration
- Store project skills in `.github/skills/`
- Version control skill directories
- Document team-specific patterns
- Share skills across projects

## Troubleshooting

**Skill not loading:**
- Check skill.yaml syntax
- Verify triggers match your query
- Ensure language is supported
- Check Copilot logs

**Skill conflicts:**
- Review trigger overlap
- Make triggers more specific
- Adjust priority in skill.yaml

**Performance issues:**
- Reduce number of active skills
- Use more specific triggers
- Optimize instructions length

## Resources

- [Agent Skills Specification](https://agentskills.io/specification)
- [Skills Directory](https://skills.sh/)
- [VS Code Agent Skills Docs](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
- [Example Skills Repository](https://github.com/anthropics/skills)

## Next Steps

1. Create `~/.copilot/skills/` directory
2. Migrate your most-used Claude skills
3. Add skill.yaml metadata
4. Test in VS Code and CLI
5. Share with team via `.github/skills/`
