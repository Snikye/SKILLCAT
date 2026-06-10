# Clean Architecture Rules

## Presentation Layer

Controllers and Minimal APIs handle only HTTP concerns:

- Route binding.
- Basic request shape validation.
- Calling application services through dependency injection.
- Returning standard HTTP responses.

Do not overload endpoints with business rules, stored procedure calls, data mapping complexity, direct configuration access, or low-level infrastructure exception handling such as direct `SqlException` catches. Infrastructure failures should flow through a global exception middleware or `IExceptionHandler` pattern.

## Application Layer

Services and use cases orchestrate application behavior:

- Business rules.
- Validation beyond basic request shape.
- Transformations and mapping between domain/DTO models.
- Coordination of repository interfaces.

Services must depend on abstractions, not concrete infrastructure implementations. Do not mix business rules with raw data access, raw file manipulation, reflection-heavy mapping, or framework-specific persistence details.

## Infrastructure Layer

Each persistence or external-provider flow should have:

- A repository/provider interface that defines the contract.
- A concrete implementation that invokes stored procedures or external services.

Repository implementations must be the only code that knows stored procedure names, SQL parameter details, command types, and database-specific mapping.

Test or development stubs/mocks must not be registered as `Singleton` when they keep mutable state or captive dependencies.

## Domain and DTO Contracts

Public service and API contracts must be strongly typed:

- Do not expose `Task<object>`.
- Do not return anonymous objects from public service contracts.
- Do not use `Dictionary<string, object?>` as a public data contract.
- Prefer C# records or sealed immutable DTO classes for request/response shapes.
- Keep infrastructure dependencies out of domain models.
- Use explicit names that describe business intent.

Strong DTOs should support compile-time safety and OpenAPI/Swagger documentation.

## Dependency Direction

Inner layers must not depend on outer layers. Business rules must not depend on controllers, database libraries, HTTP frameworks, or frontend details.
