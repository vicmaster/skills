---
name: git-conventions
description: Git commit and branching conventions. Use when creating commits or branches.
user-invocable: false
---

# Git Conventions

When creating commits:

- **Message format**: Start with a verb in imperative mood ("Add", "Fix", "Update", not "Added", "Fixes")
- **First line**: Under 72 characters, describes the "why" not the "what"
- **Body**: Add detail when the diff isn't self-explanatory — explain reasoning, trade-offs, or context
- **Scope**: One logical change per commit — don't mix refactoring with feature work
- **No generated files**: Don't commit build artifacts, lock files changes unless intentional, or IDE configs

When creating branches:

- **Format**: `type/short-description` (e.g., `feat/user-auth`, `fix/null-crash`, `refactor/api-client`)
- **Keep short**: Branch names under 40 characters
