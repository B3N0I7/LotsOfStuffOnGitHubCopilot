# Goal and attitude

- Generate C#/.NET Core code strictly applying SOLID, Clean Architecture with three layers (Domain, Application, Infrastructure), and Clean Code.
- Briefly explain architectural decisions in comments above critical classes (entities, services, handlers, repositories).
- Always suggest unit tests for Domain and integration tests for Infrastructure.
- When trade-offs exist or uncertainty arises, propose the simplest viable option and document its impact.

# Clean Architecture (Domain, Application, Infrastructure)

- Dependency rules
  - Domain depends on nothing.
  - Application depends on Domain.
  - Infrastructure depends on Domain and Application.
  - Wire dependencies at the composition root (Program/Startup of an API or service).
- Domain
  - Contains entities, value objects, aggregates, domain services, domain events, specifications.
  - Pure C# code, no framework dependencies (no EF Core, no HTTP).
  - Enforce invariants in constructors/methods.
  - Define repository interfaces and ports here or in Application as appropriate; prefer ports in Application when usage is application-oriented.
- Application
  - Contains use cases (commands/queries, handlers), DTOs, mappers, validations, orchestration, transactions (via IUnitOfWork), and ports/interfaces to external systems.
  - Uses repositories via interfaces; publishes/consumes domain events when needed.
  - No UI, no infrastructure code (no EF, no direct HTTP clients).
  - If using CQRS, separate Commands and Queries; keep handlers in Application.
- Infrastructure
  - Implements interfaces: repositories (EF Core), adapters (HTTP, message bus), providers (cache, filesystem, email, identity).
  - Configure EF Core (scoped DbContext, migrations, indexes, conversions), HttpClient via IHttpClientFactory, caching via IDistributedCache/IMemoryCache.
  - No business logic; only technical concerns and persistence mappings.

# SOLID principles

- SRP: One class, one responsibility; split services by business capability.
- OCP: Open for extension, closed for modification (polymorphism, strategies, events).
- LSP: Subtypes honor base contracts; avoid surprising exceptions on substitution.
- ISP: Small, specific interfaces; avoid “god” interfaces.
- DIP: Depend on abstractions; inject via DI; no new-ing concrete dependencies in domain/application.

# Clean Code

- Expressive naming: PascalCase for public types/methods, camelCase for variables/parameters; interface names prefixed with “I”.
- Small, cohesive, testable functions; favor early returns.
- No dead code or magic numbers; extract constants.
- Immutability for value objects; avoid shared mutable state and static business state.
- Separate mapping, validation, business logic, and data access.
- Comments for “why”, not for obvious “what”; XML docs on public APIs.

# C#/.NET Core best practices

- Nullability: enable nullable reference types; annotate properly; treat warnings as errors.
- Async: use async/await and CancellationToken; avoid sync-over-async; in libraries useAwait(false); in ASP.NET Core it’s generally not needed.
- Exceptions vs results: throw domain exceptions for invariant violations; for application flows consider Result/OneOf; don’t handle exceptions in Domain, handle in Application/Infrastructure with policies.
- DI: constructor injection; avoid service locator; use Options pattern for configuration (IOptions/IOptionsMonitor).
- Logging: use Microsoft.Extensions.Logging; structured logs with context (correlation ID); never log secrets.
- Configuration and secrets: use IConfiguration; store secrets in user-secrets/KeyVault; no plaintext secrets in code or configs.
- EF Core
  - Repositories implemented in Infrastructure; one DbContext per scope; transactions via UnitOfWork or DbContext.
  - Read queries: AsNoTracking; pagination, filtering, projection; avoid N+1; controlled navigation, no implicit lazy-loading in domain.
  - Versioned migrations; value object conversions; enforce keys/constraints.
- API/Web
  - Validate inputs (FluentValidation or data annotations) at Application boundary; ensure stable serialization (DTOs).
  - API versioning; error handling middleware; security (HTTPS, headers, rate limiting as needed).
- C# conventions
  - Async method names end with “Async”; implement IDisposable/IAsyncDisposable as needed; using/await using.
  - Prefer DateTimeOffset and UTC; decimal for monetary values; strongly typed enums or smart enums when helpful.
  - Use pattern matching; records for immutable DTOs; readonly struct for small value types; init-only setters for configuration objects.
- Performance and reliability
  - Avoid DbContext contention; add caching where appropriate; HTTP client pooling; avoid static Random; use RandomNumberGenerator for security.
  - Measure with metrics; optimize after profiling only.
- Testing
  - Domain: unit tests without mocks; property-based testing for invariants when useful.
  - Application: tests with mocked ports; cover happy paths and failures.
  - Infrastructure: integration tests (EF, HTTP) using local/in-memory resources and TestServer.
  - BDD-style naming; Arrange-Act-Assert; emphasize readability and robustness.
- Quality
  - Enable analyzers (Roslyn/StyleCop/FxCop); warnings as errors; enforce .editorconfig; remove dead code.
  - Targeted coverage on business rules; code reviews; CI pipeline with build, tests, analyzers.
- Generation directives for Copilot
  - Strictly respect layer dependencies; never reference Infrastructure from Domain or Application.
  - Provide a logical file structure with path hints as comments at the top of each snippet, without creating files.
  - For each use case, provide: Application handler, validations, tests, Infrastructure repository implementation if needed, and Domain entities/value objects.
  - Add short comments explaining architectural decisions and the SOLID principles applied.
