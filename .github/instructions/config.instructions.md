---
applyTo: "**/*.config.js,**/*.config.ts,**/config/**,**/.env.example,**/tsconfig.json,**/package.json,**/pubspec.yaml,**/pyproject.toml,**/setup.py"
---

# Configuration File Guidelines

## Environment Variables
- Use `.env` files for environment-specific configuration
- Never commit `.env` files - use `.env.example` as template
- Document all required environment variables in `.env.example`
- Use SCREAMING_SNAKE_CASE for variable names
- Validate required variables at application startup

## TypeScript Configuration (tsconfig.json)
```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true
  }
}
```

## Package Management
- Lock dependency versions in production
- Keep dependencies up to date
- Use semantic versioning properly
- Document why specific versions are pinned
- Separate dev dependencies from production dependencies

## Build Configuration
- Optimize for production (minification, tree-shaking)
- Configure source maps for debugging
- Set up proper environment-based builds
- Configure code splitting for web apps
- Enable compression and caching

## Path Aliases
```json
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@components/*": ["src/components/*"],
      "@utils/*": ["src/utils/*"],
      "@services/*": ["src/services/*"]
    }
  }
}
```

## Security Configuration
- Never commit secrets or API keys
- Use environment variables for sensitive data
- Configure CORS properly for APIs
- Set up CSP headers for web apps
- Enable HTTPS in production

## Linting & Formatting
- Configure ESLint/Pylint for code quality
- Use Prettier/Black for consistent formatting
- Enable format-on-save in editor
- Add pre-commit hooks for automatic checks
- Document any rule exceptions with justification

## Flutter/Dart (pubspec.yaml)
```yaml
name: my_app
description: A description

dependencies:
  flutter:
    sdk: flutter
  # Pin major versions
  provider: ^6.0.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^2.0.0

# Assets configuration
flutter:
  uses-material-design: true
  assets:
    - assets/images/
    - assets/fonts/
```

## Python (pyproject.toml)
```toml
[tool.poetry]
name = "my-project"
version = "0.1.0"
description = ""

[tool.poetry.dependencies]
python = "^3.11"

[tool.poetry.dev-dependencies]
pytest = "^7.0.0"
black = "^23.0.0"

[tool.black]
line-length = 88
target-version = ['py311']

[tool.pytest.ini_options]
testpaths = ["tests"]
```
