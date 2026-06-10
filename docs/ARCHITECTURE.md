# Architecture

ARC1 is organised into modules that separate concerns and allow for independent development and testing.

## Modules

- **api/** – FastAPI routers for authentication, content ingestion, recommendations, admin endpoints and health checks.
- **models/** – Pydantic schemas and SQLAlchemy ORM models for users, items, ratings and embeddings.
- **services/** – Core business logic, including recommendation algorithms, trust-floor calculations, review workflows and caching.
- **database/** – SQLAlchemy session management, migrations and connection handling.
- **tests/** – Unit and integration tests using pytest, with fixtures for database and service mocking.

## Data Flow

1. Client requests are received by the API layer (FastAPI).
2. The API layer validates input using Pydantic models and delegates to the service layer.
3. Services interact with the database layer to read/write data and call the recommendation algorithms.
4. Recommendation algorithms use user/item embeddings, rating history and trust-floor baselines to produce ranked lists.
5. The ReviewOps module allows human reviewers to inspect and adjust recommendations before final delivery.
6. Responses are returned through the API layer back to the client.

## Dependency Management

ARC1 uses dependency injection patterns from FastAPI to manage database sessions, authentication, and service instances. This allows easy swapping of components (e.g. database, caching backend) and simplifies testing.

## Asynchronous Tasks

Long-running processes such as batch embeddings generation, model training and scheduled benchmarks run in background workers using Celery or RQ and communicate with the main application via message queues like Redis.

## Caching

To improve performance and reduce latency, the service layer caches frequent queries and precomputed recommendations in Redis. Cache keys are namespaced and invalidated on updates to user or item data.

## Extensibility

The architecture is designed for extensibility; new algorithms or services can be added without breaking existing functionality. For example, you can add a content-based recommender in `services/` and register it through the API router.

## Diagram

A high-level architecture diagram can be added here using a Markdown image once you generate it (e.g., `![ARC1 Architecture](../assets/arc1-architecture.png)`).
