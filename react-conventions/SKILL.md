---
name: react-conventions
description: React and TypeScript conventions for component development. Use when writing or modifying React components.
user-invocable: false
---

# React Conventions

When writing or modifying React components:

- **Functional components only** — no class components
- **Named exports** preferred over default exports (except page components)
- **Props**: Define a `type Props = {}` above the component, not inline
- **Hooks**: Extract complex logic into custom hooks (`use` prefix)
- **State**: Prefer derived state over `useEffect` for computed values
- **Events**: Name handlers `handleX` (e.g., `handleClick`, `handleSubmit`)
- **Avoid**: Unnecessary `useMemo`/`useCallback` — only optimize when measured
- **Keys**: Never use array index as key for dynamic lists
- **Conditionals**: Use early returns over nested ternaries for readability
