# Todo API

## Questions & Answers

### 1. Role of DbContext and Dependency Injection

The `DbContext` acts as the bridge between Entity Framework Core and the database, managing database connections, querying, and updating entities (`DbSet<T>`). Registering it via Dependency Injection (DI) manages its lifecycle automatically—typically as a scoped service. This ensures each HTTP request gets its own context instance, preventing concurrency issues, promoting loose coupling, and simplifying unit testing.

### 2. What Problem a DTO Solves

A DTO (Data Transfer Object) isolates internal database schemas from the public API layer. Without DTOs, applications are vulnerable to over-posting attacks (where clients send unexpected properties to modify hidden model fields like `Secret`), over-fetching (sending unnecessary sensitive data back to the client), and tight coupling, where any change to internal entities breaks external client contracts.

### 3. Difference Between `IActionResult` and `ActionResult<T>`

`IActionResult` represents an HTTP response status code (e.g., `204 NoContent`, `404 NotFound`) without declaring a specific return type in the method signature. `ActionResult<T>` allows returning either an HTTP status code or a strongly typed object (`T`). Using `ActionResult<T>` improves API documentation (such as OpenAPI/Swagger specs) by explicitly exposing the expected response data model type.
