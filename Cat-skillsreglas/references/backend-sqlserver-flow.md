# Backend SQL Server Flow

## Non-Negotiable Persistence Rules

- Application code must not execute raw `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `MERGE`, DDL, or ad hoc SQL statements.
- Application code must not use `SELECT *` in embedded SQL because embedded SQL itself is forbidden.
- Application code must not concatenate, interpolate, or dynamically assemble SQL text.
- All database interaction must happen through parameterized stored procedure calls.
- Repository implementations are responsible for mapping strongly typed parameters and reading strongly typed results.
- Verify SQL Server parameter names, data types, nullability, sizes, precision, scale, and return shapes before changing repository contracts.

## Second-Order SQL Injection Prevention

- Do not concatenate configuration values, table names, column names, schema names, sort fields, or external parameters into persistence commands.
- If a dynamic identifier is unavoidable inside a stored procedure, require a strict allowlist and rigid validation before evaluation.
- Never pass user-controlled identifiers through the API for direct execution.
- Treat stored procedure parameters as data, not executable command fragments.

## Required Implementation Order

1. Confirm the business requirement and data contract.
2. Inspect the table/view/procedure contract if available.
3. Create or update stored procedure contract only after user approval when structural DB changes are involved.
4. Update repository interface and implementation.
5. Update service/use case orchestration.
6. Update controller or Minimal API endpoint and request/response DTOs.
7. Update frontend consumer only after API behavior is clear.

## DDL Safety Protocol

If the solution requires deleting, altering, or renaming any database object, stop immediately. Ask the user for explicit confirmation twice in two separate replies before writing DDL or migration scripts.

Examples requiring the protocol:

- `DROP TABLE`, `ALTER TABLE`, `DROP COLUMN`, column rename, table rename.
- View deletion or signature-breaking changes.
- Stored procedure deletion or signature-breaking changes.
- Changes to keys, constraints, indexes, triggers, schemas, permissions, or security policies.

## Contract Verification

Before changing API or repository behavior, verify:

- Stored procedure name and schema.
- Input parameter names and SQL types.
- Output columns, result sets, and nullable fields.
- Expected error codes, return values, and transaction behavior.
- Date/time precision, including formats such as `yyyy-MM-dd HH:mm:ss.fff`.
- Timeout expectations and retry policy boundaries.
