# 🧪 Testing Guidelines

## Current Status

- `MVCApp1.UnitTests` provides unit tests for controllers and integration tests
- `MVCApp1.PlaywrightTests` provides headless smoke coverage using Playwright against a running instance of the site
- Controllers have a coverage target of ≥90%

## How to Add Tests

1. Create a test project (e.g., `MVCApp1.Tests`):

   ```bash
   dotnet new xunit -n MVCApp1.Tests
   dotnet add MVCApp1.Tests/MVCApp1.Tests.csproj reference MVCApp1/MVCApp1.csproj
   ```

2. Add tests for controllers and services.
3. Update the solution file to include the test project:

   ```bash
   dotnet sln add MVCApp1.Tests/MVCApp1.Tests.csproj
   ```

## Running Tests

- Locally: `dotnet test`
- Playwright browsers (first run): `dotnet build tests/MVCApp1.PlaywrightTests` followed by `pwsh bin/Debug/net9.0/playwright.ps1 install` or simply execute the tests once and the suite will install browsers automatically.
- CI (GitHub Actions): Automatically installs Playwright via `Microsoft.Playwright.CLI` and runs `dotnet test` when test projects exist.

## Test Structure

### Unit Tests (`MVCApp1.UnitTests`)
- Controller tests with mocked dependencies
- Service tests (when services are added)
- Integration tests for application startup

### End-to-End Tests (`MVCApp1.PlaywrightTests`)
- Smoke tests for critical user flows
- Browser-based testing with Playwright
- Tests against actual running application

## Guidelines

- Use AAA (Arrange-Act-Assert) pattern.
- Mock dependencies (e.g., `ILogger<T>`, services) where appropriate.
- Keep tests deterministic and isolated.
- Use `WebApplicationFactory<Program>` for integration tests.
- Test both success and error paths.
- Name tests descriptively: `MethodName_Scenario_ExpectedBehavior`.
