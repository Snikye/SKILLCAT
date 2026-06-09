# Audit Quality Rules

## Static Analysis Readiness

Write code that can pass strict SAST, SonarQube, Snyk, and AI-assisted review:

- Avoid duplication.
- Remove unused imports, dead branches, unused variables, and stale routes.
- Prefer small methods with clear responsibilities.
- Use guard clauses to reduce nested conditionals.
- Keep cyclomatic complexity low.
- Use explicit names that describe business intent.

## Comments

Comments should explain why a business rule, security decision, or architectural constraint exists. Do not add comments that merely restate the syntax.

## Refactoring Discipline

- Follow existing project conventions unless they conflict with security or correctness.
- Keep changes scoped to the requested behavior.
- Do not perform broad rewrites unless explicitly requested.
- Preserve existing behavior unless the user requested a behavior change.

## Final Self-Review

Before responding, check:

- No direct SQL or forbidden dependency was introduced.
- No secrets, credentials, stack traces, or internal details are exposed.
- Layer boundaries are respected.
- Validation path is documented.
- Remaining risks or assumptions are named clearly.
