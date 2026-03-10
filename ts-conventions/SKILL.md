---
name: ts-conventions
description: TypeScript conventions and patterns. Use when writing or modifying TypeScript code.
user-invocable: false
---

# TypeScript Conventions

When writing TypeScript:

- **Prefer `type` over `interface`** unless declaration merging is needed
- **Avoid `any`** — use `unknown` and narrow, or define a proper type
- **Avoid `enum`** — use `as const` objects or union types instead
- **Avoid non-null assertions (`!`)** — handle the null case explicitly
- **Use `satisfies`** when you want to validate a type without widening
- **Generics**: Name them descriptively (`TItem`, `TResult`) not just `T` when there are multiple
- **Return types**: Let TypeScript infer return types for simple functions; annotate explicitly for public APIs or complex functions
- **Narrowing**: Prefer type guards and discriminated unions over type casting
