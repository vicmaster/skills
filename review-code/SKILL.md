---
name: review-code
description: Review recently changed files for bugs, security issues, and code quality
disable-model-invocation: true
argument-hint: [file-or-scope]
---

# Review Code

Review the code changes for quality and correctness.

## Instructions

1. Identify files to review:
   - If `$ARGUMENTS` is a file path, review that file
   - If `$ARGUMENTS` is "staged" or empty, review `git diff --cached`
   - If `$ARGUMENTS` is "recent", review uncommitted changes via `git diff`
2. For each file, check for:
   - **Bugs**: Logic errors, off-by-one, null/undefined access, race conditions
   - **Security**: Injection, XSS, hardcoded secrets, missing validation
   - **Performance**: Unnecessary loops, missing indexes, N+1 queries, memory leaks
   - **Style**: Naming, consistency with surrounding code, dead code
3. Provide findings as a numbered list with file path, line number, severity (critical/warning/info), and suggested fix
4. If no issues found, confirm the code looks good
