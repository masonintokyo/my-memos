## 0. Goals

* **Loose Coupling**: Components communicate strictly through explicit interfaces. Internal implementations must not leak across boundaries.
* **High Modularity**: Single Responsibility Principle (SRP) and Dependency Inversion Principle (DIP). A pluggable structure that allows interchangeable components.
* **Ease of Extension**: New features should ideally be *added* without modifying existing code (Open/Closed Principle).
* **Testability**: Automated execution of unit and integration tests, reproducible in CI.
* **Observability**: Standardized logging, metrics, and tracing.

## 1. Architectural Principles

* **SOLID** (with emphasis on SRP / OCP / LSP / ISP / DIP)
* **Clean Architecture**: Use Case (application) ← Port (abstraction) → Adapter (implementation)
* **Contract-Driven Design**: Define interfaces first, then plug in implementations later.
* **Configuration over Code**: Wire concrete instances using a DI container or factory. Isolate environment-dependent values in `.env`.
* **Defensive Design**: Contracts should include input validation, error classification, timeouts, and retry policies.

## Principles Agents Must Follow

1. **Restrictions on External Input**
   * Do not fetch unclassified URLs or dependencies.
   * Use only domains and dependencies on the approved list.

2. **Output Safety**
   * Do not output secrets or internal information.
   * Do not change workflows or permission settings.
   * Do not include diffs that would trigger automatic execution (such as external communication or dependency additions).

3. **Network Usage**
   * Outbound communication must be limited to the minimum necessary GET/HEAD/OPTIONS requests.
   * Do not send data to unapproved external services.

4. **Dependencies and Artifacts**
   * Only use new dependencies that can be signature-verified.
   * Do not use unsigned binaries or images without approval.

5. **Respect for the Execution Environment**
   * Do not obtain credentials from IMDS (cloud metadata services).
   * Do not access secrets within the execution environment.

6. **Transparency**
   * All actions that touch external systems must be logged.
   * Outputs must clearly state sources and intent.

## Documentation Maintenance

- Whenever code is added or modified, ensure the user-facing instructions (`docs/USER_INSTRUCTIONS.md`) and both developer guides (`docs/DEVELOPER_OVERVIEW.md`, `docs/DEVELOPER_GUIDE.md`) are reviewed and updated to reflect the new behavior before completing the change.
