# Security Rules

## Secrets and Configuration

- Never hardcode JWT keys, API keys, connection strings, credentials, tokens, certificates, or default production secrets.
- Read secrets from secure configuration, environment variables, container secrets, or an approved secret manager.
- Validate required secrets during startup.
- Signing keys and credentials must satisfy project-defined length, entropy, rotation, and custody requirements.

## Sensitive Comparisons

Use constant-time comparison for API keys, tokens, signatures, or cryptographic secrets.

For .NET, prefer `CryptographicOperations.FixedTimeEquals` with normalized byte arrays. Do not compare sensitive strings with `==`, `!=`, `.Equals`, or direct case-insensitive comparison.

## Error Handling

- Return generic, sanitized error responses to clients.
- Do not expose stack traces, SQL errors, filesystem paths, raw parameters, tokens, claims, native database messages, or internal exception messages.
- Log enough diagnostic detail for operators, but exclude or mask secrets and sensitive data.
- Route infrastructure exceptions through global exception handling rather than duplicating low-level catch blocks in endpoints.

## Authorization and Input

- Validate authorization at the API boundary and service layer where business rules require it.
- Validate input shape, length, format, and allowed ranges before persistence.
- Use guard clauses for invalid or unauthorized flows.
- Do not trust frontend validation as a security boundary.

## OWASP Orientation

Check changes against OWASP Top 10 concerns, especially injection, broken access control, cryptographic failures, insecure design, security misconfiguration, vulnerable dependencies, authentication failures, integrity failures, logging failures, and SSRF.
