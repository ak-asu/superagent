---
applyTo: "**/*.ts,**/*.tsx"
---

# TypeScript Code Guidelines

## Type Safety
- Enable strict mode in tsconfig.json
- Avoid using `any` type - use `unknown` if type is truly unknown
- Use type guards for narrowing
- Prefer interfaces for objects, types for unions/intersections

## Patterns
- Use optional chaining (`?.`) and nullish coalescing (`??`)
- Destructure objects and arrays for cleaner code
- Use const assertions for literal types
- Leverage discriminated unions for state

## Async Code
- Prefer async/await over .then() chains
- Always handle Promise rejections
- Use Promise.all() for parallel operations
- Type async function return values explicitly

## React (TSX)
- Type component props with interfaces
- Use React.FC sparingly (prefer explicit return types)
- Type event handlers properly
- Use generics for reusable components
