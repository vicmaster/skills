---
name: test-writer
description: Write or update tests for changed code. Use when implementing features or fixing bugs.
disable-model-invocation: true
argument-hint: [file-or-function]
---

# Test Writer

Write tests for $ARGUMENTS.

## Instructions

1. Read the source code to understand what it does
2. Identify the project's test framework (Jest, Vitest, Mocha, pytest, etc.) by checking config files and existing tests
3. Find existing tests for the module — update them if they exist, create a new test file if not
4. Write tests covering:
   - **Happy path**: Normal expected usage
   - **Edge cases**: Empty input, null, boundary values, large inputs
   - **Error cases**: Invalid input, missing data, network failures
5. Follow the patterns of existing tests in the project (naming, structure, assertions)
6. Run the tests to verify they pass
