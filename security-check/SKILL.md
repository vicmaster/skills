---
name: security-check
description: Security patterns and common vulnerabilities to watch for. Use when writing code that handles user input, authentication, or external data.
user-invocable: false
---

# Security Check

When writing code that handles user input, auth, or external data:

- **Never trust input**: Validate and sanitize all user input at system boundaries
- **SQL**: Use parameterized queries — never string concatenation
- **HTML**: Escape output to prevent XSS — use framework-provided methods (React does this by default, but watch for `dangerouslySetInnerHTML`)
- **Secrets**: Never hardcode API keys, tokens, or passwords — use environment variables
- **Auth**: Compare tokens/passwords with constant-time comparison to prevent timing attacks
- **File paths**: Validate and resolve paths to prevent directory traversal (`../`)
- **Dependencies**: Prefer well-maintained packages — flag any dependency with known vulnerabilities
- **Errors**: Don't expose stack traces or internal details in user-facing error messages
- **CORS**: Be explicit about allowed origins — never use `*` in production
