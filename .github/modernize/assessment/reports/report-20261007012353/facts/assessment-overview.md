# Assessment Overview

Supplementary documents present in this report's facts directory:

| Document | Description |
|---|---|
| [Architecture diagram](architecture-diagram.md) | Application layers, storage/integration boundaries and component relationships with two Mermaid diagrams. |
| [Dependency map](dependency-map.md) | Declared Maven dependencies, parent-managed versions, scope counts and compatibility caveats. |
| [API and service contracts](api-service-contracts.md) | Service catalog, five explicit endpoints, response contracts, security posture and request sequence. |
| [Data architecture](data-architecture.md) | Oracle/H2 configuration, photo entity model, repository methods, data ownership and sensitivity. |
| [Configuration inventory](configuration-inventory.md) | Configuration sources/profiles, property defaults, startup/resources and redacted secret provisioning workflows. |
| [Business workflows](business-workflows.md) | Upload, browsing/navigation and deletion flows, validation rules and partial-result behavior. |

These are static, source-evidenced documents, not runtime/deployment verification. Literal credentials are redacted. No tests or deployment commands were run; Mermaid rendering was not exercised. Oracle Free Compose definitions differ from older README Oracle XE descriptions. Azure PostgreSQL provisioning is not integrated with the current Oracle application stack.

Automated cloud-readiness and upgrade findings are heuristic and require contextual verification. Scanner support assertions are not established facts; for example, Java 8 support depends on the vendor/distribution and applicable support terms.
