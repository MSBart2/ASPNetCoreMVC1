# ✍️ Coding & Documentation Conventions

## C# Style

- **Nullable enabled**: Use `string?` where appropriate.
- **Implicit usings**: Keep files clean; avoid redundant usings.
- **Namespaces**: `MVCApp1.*` (file-scoped preferred).
- **Logging**: Inject `ILogger<T>`; log at appropriate levels.
- **Exceptions**: Prefer specific exception types; avoid swallowing exceptions.
- **Async/Await**: Use async methods for I/O operations; suffix with `Async`.
- **Dependency Injection**: Use constructor injection for services.

## XML Documentation

- All **public** classes/methods/properties **must** have `///` XML comments.
- Summaries should be concise, starting with a verb.
- Include `<param>`, `<returns>`, and `<remarks>` when helpful.
- Include `<exception>` tags for thrown exceptions.
- The build generates `MVCApp1.xml` (see `MVCApp1.csproj`).

### Example
```csharp
/// <summary>
/// Searches for results matching the query criteria.
/// </summary>
/// <param name="query">The search query parameters.</param>
/// <returns>A list of search results.</returns>
/// <exception cref="ArgumentNullException">Thrown when query is null.</exception>
Task<List<SearchResult>> SearchAsync(SearchQuery query);
```

## Controllers & Actions

- Return appropriate `IActionResult` (e.g., `View()`, `RedirectToAction`).
- Apply attributes for caching, authorization, and routing explicitly.
- Validate inputs and model state (`ModelState.IsValid`).
- Use dependency injection for services (constructor injection).
- Use `[FeatureGate]` attribute for feature-flagged actions.
- Apply `[ValidateAntiForgeryToken]` on POST actions to prevent CSRF.

## Views

- Use strongly-typed models where possible (`@model` directive).
- Keep logic in controllers/services; minimize code in views.

## Configuration

- Use `appsettings.json` and environment-specific overrides (e.g., `appsettings.Development.json`).
- Do **not** commit secrets; use environment variables or secret managers.
- Use Azure App Configuration for centralized configuration and feature flags in production.
- Access configuration via `IConfiguration` dependency injection.

## Testing

- Name test projects `*.Tests`.
- Use `dotnet test` and keep tests idempotent.
- Prefer unit tests for controllers/services; add integration tests for key flows.

## Git Hygiene

- `.gitignore` excludes build artifacts, secrets, IDE files.
- Commit small, focused changes with clear messages.

## Documentation Process

- Update `README.md` and relevant docs in `docs/` for notable changes.
- The **Documentation Helper** agent will flag missing XML docs on new public code.
