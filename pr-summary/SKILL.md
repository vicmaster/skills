---
name: pr-summary
description: Summarize changes in a pull request with context, risks, and review notes
disable-model-invocation: true
argument-hint: [pr-number]
context: fork
agent: Explore
allowed-tools: Bash(gh *)
---

# PR Summary

## Pull request context

- PR diff: !`gh pr diff $ARGUMENTS`
- PR description: !`gh pr view $ARGUMENTS`
- Changed files: !`gh pr diff $ARGUMENTS --name-only`

## Your task

Summarize this pull request:

1. **What changed**: Brief overview of the changes (2-3 sentences)
2. **Key files**: List the most important files changed and why
3. **Risks**: Anything that could break — edge cases, missing tests, breaking changes
4. **Review notes**: Specific things a reviewer should pay attention to
