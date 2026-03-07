---
name: fix-build
description: Fix build failures by reading errors and patching the failing files
disable-model-invocation: true
argument-hint: [error-output]
---

# Fix Build

When the build fails, diagnose and fix the issue.

## Instructions

1. Run the project's build command (check `package.json` scripts, `Makefile`, or common build tools)
2. Read the error output carefully — identify the failing file(s) and line number(s)
3. Read the failing file(s) to understand the context
4. Fix the root cause (don't just suppress the error)
5. Run the build again to verify the fix
6. If new errors appear, repeat until the build succeeds
