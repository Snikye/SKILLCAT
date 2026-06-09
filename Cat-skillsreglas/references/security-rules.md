# Security Rules

## Secrets and Configuration

- Never hardcode JWT secrets, API keys, connection strings, credentials, tokens, or default production secrets.
- Read secrets from secure configuration, environment variables, container secrets, or an approved secret manager.
- Validate required secrets during startup.
- Secrets used for signing should be at least 32 characters unless the project defines a stronger requirement.

## Sensitive Comparisons

Use constant-time comparison for API keys, tokens, signatures, or cryptographic secrets.

For .NET, prefer `CryptographicOperations.FixedTimeEquals` with normalized byte arrays. Do not compare sensitive strings with `==`, `!=`, `.Equals`, or direct case-insensitive comparison.

## Error Handling

- Return generic, sanitized error responses to clients.
- Do not expose stack traces, SQL errors, filesystem paths, raw parameters, tokens, claims, or internal exception messages.
- Log enough diagnostic detail for operators, but exclude or mask secrets and sensitive data.
- Use specific catch blocks when they help separate expected business failures from infrastructure failures.

## Authorization and Input

- Validate authorization at the API boundary and service layer where business rules require it.
- Validate input shape, length, format, and allowed ranges before persistence.
- Use guard clauses for invalid or unauthorized flows.
- Do not trust frontend validation as a security boundary.

## OWASP Orientation

Check changes against OWASP Top 10 concerns, especially injection, broken access control, cryptographic failures, insecure design, security misconfiguration, vulnerable dependencies, authentication failures, integrity failures, logging failures, and SSRF.
