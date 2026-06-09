# Frontend and Ecosystem Rules

## HTTP Client

Do not introduce `axios`. Prefer native `fetch` wrapped in a project-level client that handles:

- Base URL resolution.
- Auth headers or credentials policy.
- Timeout/abort behavior when supported by the project.
- JSON parsing.
- Standardized error handling.
- Sanitized user-facing error messages.

If the project already has an approved HTTP wrapper, use it.

## NPM Dependencies

Before adding Node dependencies:

- Prefer existing project dependencies.
- Avoid alpha, beta, rc, deprecated, or low-trust packages.
- Prefer stable, maintained packages with clear versioning.
- Run the project dependency audit workflow when available.

## Frontend Boundary

Frontend code must call the REST API. It must not bypass the backend, connect directly to SQL Server, encode secret business rules as the only enforcement point, or store backend secrets.
