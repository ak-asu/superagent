---
applyTo: "**/*.dart"
---

# Flutter/Dart Code Guidelines

## Widget Best Practices
- Use const constructors wherever possible
- Keep widgets small and focused
- Extract complex widgets into separate files
- Prefer composition over inheritance

## State Management
- Use stateless widgets when no local state needed
- Keep state as close to where it's used as possible
- Use BLoC/Cubit for complex state
- Avoid excessive rebuilds

## Naming Conventions
- Use lowerCamelCase for variables, functions
- Use UpperCamelCase for classes, enums
- Prefix private members with underscore
- Use descriptive names for callbacks

## Code Organization
- One widget per file (for complex widgets)
- Group related files in feature folders
- Use barrel files (index.dart) for exports
- Keep business logic separate from UI

## Performance
- Use const widgets where possible
- Implement shouldRebuild for complex conditions
- Use ListView.builder for long lists
- Avoid unnecessary widget tree depth
