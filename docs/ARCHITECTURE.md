# Architecture overview

ARC1 is a proposed microservices-based recommendation platform.  This document describes the high-level components and data flow of the system.  Please note that these modules are **conceptual** only – there is no running code in the repository yet.

## Components

- **API Gateway** – exposes REST endpoints for authentication, browsing and recommendations.  Planned to be implemented with Python and FastAPI.
- **Authentication service** – manages user registration, login and token issuance.
- **Recommendation service** – hosts the core recommendation algorithms and business logic.
- **Data ingestion** – responsible for importing and updating catalog data from external sources.
- **ReviewOps** – a proposed human-in-the-loop process for evaluating algorithm changes before deployment.
- **Database** – stores users, items, ratings and event logs.  Technology choices are still under consideration.

## Data flow

1. Clients send requests to the API gateway (e.g., to register a user or request recommendations).
2. The API gateway forwards authentication requests to the authentication service and content/recommendation requests to the relevant service.
3. The recommendation service retrieves user and item metadata from the database and applies collaborative filtering or hybrid models to generate a ranked list.
4. The review process (once implemented) will allow manual review of new algorithms before they go live.

---

*This architecture description outlines planned components as of June 2026.  The ARC1 repository currently contains only design documentation; there is no `src/` directory or executable code.*
