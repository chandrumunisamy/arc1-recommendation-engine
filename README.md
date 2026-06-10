# ARC1 Recommendation Engine

ARC1 is an AI-powered backend recommendation system that delivers personalized content to users. It is built with **FastAPI** and designed to be modular, scalable, and production-ready. Features include authentication, content APIs, user/item embeddings, trust-floor baseline algorithms, a ReviewOps workflow, comprehensive tests, and benchmarks.

## Features

- **Modular design**: Clear separation of services for authentication, content ingestion, recommendations, etc.
- **FastAPI**: High-performance Python web framework used to build RESTful APIs.
- **Authentication & Authorization**: JWT-based user authentication and role-based access controls.
- **Content and User APIs**: CRUD endpoints for items, ratings, user profiles, and interactions.
- **Recommendation Algorithms**: Implements collaborative filtering and trust-floor algorithms for robust recommendations.
- **ReviewOps workflow**: A review operations module that allows human-in-the-loop review and adjustment of recommendations.
- **Testing & Benchmarking**: Comprehensive test suite with pytest and benchmarking scripts to compare algorithm performance.
- **CI/CD ready**: Configured for continuous integration with GitHub Actions.

## Architecture

ARC1 is organized into a **src** directory with submodules:

- `api/` – FastAPI routers for auth, content, recommendations.
- `models/` – Pydantic models and ORM models.
- `services/` – Business logic for recommendations, trust-floor algorithms and review workflows.
- `database/` – SQLAlchemy models and database utilities.
- `tests/` – Unit and integration tests.

A high-level architecture diagram is provided in [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Getting Started

### Prerequisites

- Python 3.10+
- PostgreSQL database
- Redis (for caching and task queues)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/chandrumunisamy/arc1-recommendation-engine.git
   cd arc1-recommendation-engine
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # or `\.\venv\Scripts\activate` on Windows
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file based on [.env.example](.env.example) and update the environment variables for your database and secret keys.

5. Run database migrations:
   ```bash
   alembic upgrade head
   ```

6. Start the development server:
   ```bash
   uvicorn src.main:app --reload
   ```

Visit `http://localhost:8000/docs` to explore the interactive API documentation.

## API Examples

Create a new user:

```http
POST /api/v1/users
Content-Type: application/json

{
  "username": "alice",
  "password": "secret"
}
```

Get personalized recommendations for a user:

```http
GET /api/v1/recommendations?user_id=1&top_k=10
```

More detailed API endpoints and example payloads are described in [docs/API.md](docs/API.md).

## Testing

Run the test suite with:
```bash
pytest
```

To run tests with coverage:
```bash
pytest --cov=src --cov-report=term-missing
```

## Benchmarks

Benchmark scripts and results can be found in [docs/BENCHMARKS.md](docs/BENCHMARKS.md). These benchmarks compare collaborative filtering to trust-floor algorithms on synthetic and real datasets.

## ReviewOps

The ReviewOps module allows human-in-the-loop moderation of recommendations. See [docs/REVIEWOPS.md](docs/REVIEWOPS.md) for details on the workflow and how to integrate it into your systems.

## Roadmap

- [ ] Add content-based filtering algorithms
- [ ] Implement A/B testing framework for recommendations
- [ ] Integrate asynchronous task queues
- [ ] Deploy on Kubernetes with Helm charts
