---
name: minimal-changes
description: Enforce minimal, focused changes — avoid over-engineering, unnecessary refactoring, or scope creep
user-invocable: false
---

# Minimal Changes

When implementing a task:

- **Do exactly what was asked** — no bonus features, no "while I'm here" refactors
- **Don't add abstractions for one use case** — three similar lines is better than a premature helper
- **Don't add error handling for impossible scenarios** — trust internal code and framework guarantees
- **Don't add comments for obvious code** — only comment when the "why" isn't clear from the code
- **Don't add type annotations to unchanged code** — only type what you're touching
- **Don't rename variables in code you didn't change** — cosmetic changes add noise to diffs
- **Don't add feature flags or backwards-compatibility shims** — just change the code
- **If you removed something, remove it completely** — no `// removed`, no `_unused` vars, no re-exports
