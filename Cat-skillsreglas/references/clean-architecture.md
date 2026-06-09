# Clean Architecture Rules

## Controllers

Controllers handle only HTTP concerns:

- Route binding.
- Basic request shape validation.
- Calling application services through dependency injection.
- Returning standard HTTP responses.

Controllers must not contain business rules, stored procedure calls, data mapping complexity, or infrastructure decisions.

## Services

Services orchestrate application behavior:

- Business rules.
- Validation beyond basic request shape.
- Transformations and mapping between domain/DTO models.
- Coordination of repository interfaces.

Services must depend on abstractions, not concrete infrastructure implementations.

## Repositories

Each persistence flow should have:

- A repository interface that defines the contract.
- A concrete implementation that invokes stored procedures.

Repository implementations must be the only code that knows stored procedure names, SQL parameter details, command types, and database-specific mapping.

## Models and DTOs

Models and DTOs should be explicit and purpose-driven:

- Avoid generic names such as `data`, `obj`, `temp`, or `info`.
- Keep infrastructure dependencies out of domain models.
- Prefer request/response DTOs when API contracts differ from domain objects.

## Dependency Direction

Inner layers must not depend on outer layers. Business rules must not depend on controllers, database libraries, HTTP frameworks, or frontend details.
