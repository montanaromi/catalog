---
title: "Prevent Security Vulnerabilities"
description: "Ensure generated code follows security best practices and never introduces common vulnerability patterns"
icon: "shield-halved"
---

## When to Use

Add this to enforce secure coding practices across all code generation for a project, preventing common vulnerability patterns from being introduced.

## Rule Definition

**Name** — Prevent Security Vulnerabilities

**Description** — paste this into the rule description field on the platform:

```
All generated code MUST follow security best practices. MUST NOT introduce code that contains known vulnerability patterns.

Requirements:
- Use parameterized queries or prepared statements for all database access — MUST NOT concatenate user input into SQL, NoSQL, or ORM queries
- Use environment variables or a secrets manager for all credentials, tokens, API keys, and connection strings — MUST NOT hardcode secrets
- Validate and sanitize all external input (user input, API parameters, file uploads, webhook payloads) before processing
- Use the framework's built-in escaping for all rendered output to prevent XSS — MUST NOT insert raw user content into HTML, templates, or DOM
- Apply the principle of least privilege for all authentication and authorization checks — MUST NOT grant broad access when narrow access is sufficient
- Use strong, current cryptographic algorithms and proper key management — MUST NOT use deprecated algorithms (MD5, SHA1 for security, DES, RC4)
- Pin dependency versions and avoid adding dependencies with known CVEs
- Set timeouts, rate limits, and size limits on all external service calls and user-facing endpoints

Forbidden Patterns:
- String concatenation or interpolation in SQL, command-line, or template expressions that include external input
- Hardcoded passwords, tokens, API keys, or connection strings anywhere in source code
- Rendering user-supplied content without escaping or sanitization
- Disabled or bypassed authentication/authorization checks, even temporarily
- Catching and silently discarding security-related exceptions
- Using `eval()`, `exec()`, or equivalent dynamic code execution with external input
- Storing sensitive data (passwords, tokens, PII) in logs, error messages, or client-facing responses

Validation Gate: Generated code that introduces any forbidden pattern fails review. Every database query MUST use parameterized access. Every credential MUST reference an environment variable or secrets manager. Every endpoint accepting external input MUST validate that input before processing.

Verification: No forbidden security pattern is present, all queries use parameterized access, and all credentials reference environment variables or a secrets manager.
Scope: Applies to all generated code that handles database access, user input, authentication, cryptography, or external service calls.
```

## How It Works

1. Add this rule to your project on the platform
2. All generated code automatically follows secure coding practices
3. Database queries use parameterized access, secrets are externalized, input is validated
4. Forbidden vulnerability patterns are never introduced in generated code
5. Code review validates that security constraints are met across all generated files
