# Audit Quality Rules

## Static Analysis Readiness

Write code that can pass strict SAST, AST, SonarQube, Snyk, npm audit, and AI-assisted review:

- Avoid duplication.
- Remove unused imports, dead branches, unused variables, stale routes, deprecated methods, and orphan code.
- Prefer small methods with clear responsibilities.
- Use guard clauses to reduce nested conditionals and loops.
- Keep cyclomatic complexity low, linear, and easy to scan.
- Use explicit names that describe business intent.

## Shared Utilities

Do not duplicate common helper routines such as text normalization, SQL formatting, sanitization, date parsing, or conversion logic across local classes. Centralize cross-cutting utilities in an approved shared building-blocks library or existing project helper.

## Robust Parsing

Parsing routines must be explicit and resilient:

- Prefer strict parsing such as `DateTime.TryParseExact` when the expected format is known.
- Support high-precision database date formats such as `yyyy-MM-dd HH:mm:ss.fff` when relevant.
- Add safe fallbacks for ISO or regional formats when the business flow needs tolerance.
- Do not silently drop records when parsing fails; surface controlled diagnostics or validation results.

## Comments

Comments should explain why a business rule, security decision, or architectural constraint exists. Do not add comments that merely restate syntax.

## Refactoring Discipline

- Follow existing project conventions unless they conflict with security or correctness.
- Keep changes scoped to the requested behavior.
- Do not perform broad rewrites unless explicitly requested.
- Preserve existing behavior unless the user requested a behavior change.

## Final Self-Review

Before responding, check:

- No direct SQL, second-order SQL injection path, or forbidden dependency was introduced.
- No secrets, credentials, stack traces, native database errors, or internal details are exposed.
- Layer boundaries are respected.
- DTO contracts are explicit and strongly typed.
- Validation path is documented.
- Remaining risks, assumptions, and production optimization suggestions are named clearly.
