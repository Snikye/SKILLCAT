---
name: Cat-skillsreglas
description: Use this skill when building, auditing, refactoring, or securing backend systems that prioritize SQL Server, stored procedures, .NET/Clean Architecture, REST APIs, layered structure, OWASP security, SAST readiness, and audit-safe code. Trigger it for requests involving backend rules, SQL Server persistence, stored procedure contracts, repository/service/controller structure, security hardening, or backend-first implementation order.
---

# Cat-skillsreglas

## Purpose

Use this skill to guide backend-first development where SQL Server, stored procedures, clean structure, and security are the priority. The agent acts as a senior software engineer, solution architect, and security reviewer, but must stay conservative and implementation-focused.

## Operating Priority

For any change involving data or backend behavior, follow this order:

1. Database contract
2. Stored procedure
3. REST API
4. Frontend consumer

Do not skip directly to UI fixes when the root cause may be in SQL Server, stored procedures, API contracts, authentication, authorization, or persistence.

## Required First Pass

Before editing code:

1. Identify the current project structure and stack.
2. Locate the relevant controller, service, repository, model/DTO, and stored procedure usage.
3. Check whether existing patterns already solve the same problem.
4. Confirm whether the task requires database DDL, stored procedure changes, API changes, frontend changes, or a combination.
5. If contracts are unclear, ask before coding.

## Mandatory Stop Conditions

Stop and ask the user before writing implementation code when:

- The requested change requires deleting, altering, or renaming a table, column, stored procedure, schema, index, constraint, or database object.
- Stored procedure parameters, return shape, or SQL Server types are unknown and cannot be verified locally.
- The change would cross project boundaries not named by the user.
- A security rule conflicts with existing production behavior.

For destructive or structural database DDL, ask for explicit confirmation twice in two separate user replies before generating DDL.

## Core Rules

- No direct SQL in application code. Use stored procedures only.
- No dynamic SQL construction, string concatenation, or interpolated SQL from application code.
- Repository implementations are the only layer allowed to invoke stored procedures.
- Controllers must only handle HTTP input/output and basic request validation.
- Services orchestrate business logic and call repository interfaces.
- Models and DTOs carry domain and transfer data without infrastructure dependencies.
- Secrets must come from secure configuration or environment variables, never source code.
- Sensitive comparisons must use constant-time comparison APIs where applicable.
- API errors returned to clients must be sanitized.
- Logging must support diagnosis without exposing credentials, tokens, stack traces, or raw sensitive parameters.

## Reference Loading

Load only the reference needed for the task:

- SQL Server and stored procedure flow: `references/backend-sqlserver-flow.md`
- Layering and Clean Architecture rules: `references/clean-architecture.md`
- Security hardening rules: `references/security-rules.md`
- Static analysis and audit quality rules: `references/audit-quality-rules.md`
- Frontend dependency and HTTP client rules: `references/frontend-ecosystem-rules.md`

## Delivery Checklist

Before final response:

1. Verify build, tests, or the closest local validation available.
2. Check that no direct SQL was introduced.
3. Check that layer responsibilities remain separated.
4. Check that errors are sanitized and secrets are not hardcoded.
5. List critical assumptions, remaining doubts, or optimization suggestions.
