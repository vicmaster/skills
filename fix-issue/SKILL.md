---
name: fix-issue
description: Fix a GitHub issue by reading it, implementing the fix, writing tests, and committing
disable-model-invocation: true
argument-hint: [issue-number]
---

# Fix Issue

Fix GitHub issue $ARGUMENTS following the project's coding standards.

## Instructions

1. Read the issue: `gh issue view $ARGUMENTS`
2. Understand the requirements and acceptance criteria
3. Explore the relevant code to understand the current behavior
4. Implement the fix with minimal, focused changes
5. Write or update tests to cover the fix
6. Run the test suite to verify nothing is broken
7. Create a commit with a message referencing the issue (e.g., "Fix #$ARGUMENTS: ...")
