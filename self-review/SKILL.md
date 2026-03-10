---
name: self-review
description: Verify your own work before finishing — run tests, check edge cases, and confirm nothing is broken
user-invocable: false
---

# Self-Review Checklist

Before reporting that a task is complete, verify the following:

1. **Tests pass**: Run the project's test suite. If no tests exist for the changed code, mention it.
2. **Build succeeds**: Run the build command if applicable.
3. **Edge cases**: Consider at least 2 edge cases for the change (empty input, null, boundary values, concurrent access).
4. **No leftover debug code**: Remove any console.log, debugger, TODO comments, or commented-out code you added.
5. **Types are correct**: If TypeScript, ensure no `any` types were introduced unless unavoidable.
6. **Imports are clean**: No unused imports added.

If any check fails, fix it before reporting completion. Do not ask the user — just fix it.
