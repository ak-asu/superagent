---
applyTo: "**/*.py"
---

# Python Code Guidelines

## Type Hints
- Add type hints to all function signatures
- Use `Optional[T]` for nullable parameters
- Use `Union[A, B]` or `A | B` (3.10+) for multiple types
- Import types from `typing` module

## Style
- Follow PEP 8 conventions
- Use f-strings for string formatting
- Prefer list/dict comprehensions when readable
- Use `pathlib.Path` for file operations

## Error Handling
- Use specific exception types
- Provide context in error messages
- Use context managers for resources
- Log exceptions with traceback

## Structure
- Use dataclasses for data containers
- Use Pydantic for validation
- Keep functions pure when possible
- Document with docstrings (Google style)
