# Architectural & Project Decisions

This document records the architectural and project-level decisions for the Task Management API project as of its initial setup.

## 1. Core Architectural Choices

### Backend Framework: Django and Django REST Framework
-   **Decision:** Use Django for the web framework and Django REST Framework (DRF) to build the REST API.
-   **Rationale:** Django offers rapid development with a robust set of features like an ORM and admin panel. DRF is a powerful and flexible toolkit for building Web APIs, which is the primary purpose of this project. This combination is well-supported and scalable.

### Database: PostgreSQL
-   **Decision:** Use PostgreSQL as the primary database.
-   **Rationale:** PostgreSQL is a powerful, open-source relational database known for reliability and performance. It is fully supported by Django and well-suited for complex applications.

### Containerization: Docker and Docker Compose
-   **Decision:** Use Docker to containerize the application and Docker Compose to manage services.
-   **Rationale:** This provides a consistent and isolated environment for development, testing, and production, simplifying setup for new developers and eliminating environment-specific issues.

## 2. Project Execution & Status

### Features Completed & Why
-   **Initial Project Scaffolding:** A new Django project was created with a `config` app for settings and URLs.
-   **Docker Integration:** The project is fully containerized with a `django-backend` service and a `postgres` database service.
-   **Dependency Management:** `requirements.txt` is set up with core dependencies (`Django`, `djangorestframework`, `psycopg2-binary`).
-   **Environment-based Configuration:** The application is configured using environment variables, which is a security best practice.
-   **Why:** These features form the foundational infrastructure for the application. Completing them first ensures a stable and reproducible development environment before any business logic is implemented.

### Features Skipped & Why
-   **API Endpoints:** No specific API endpoints (e.g., for creating or listing tasks) have been created yet. This was skipped to focus on establishing the project's core infrastructure first.
-   **User Authentication:** API-level authentication (e.g., JWT or Token-based) has not been implemented. This will be a subsequent step.
-   **Redis Cache/Broker:** The `redis` service is present in `docker-compose.yml` but is commented out. It was skipped because it is not required for the initial setup. It can be enabled later for caching or as a message broker for background tasks with Celery.
-   **Automated Tests:** No testing framework has been configured yet. This is a critical next step but was deferred to get the basic application running first.

### Time Allocation Breakdown (Estimated)
-   **Project Analysis & Exploration:** 25%
-   **Docker & Database Configuration:** 35%
-   **Django Project Setup:** 20%
-   **Documentation (`README.md`, `DECISIONS.md`):** 20%

## 3. Challenges & Trade-offs

### Technical Challenges Faced
-   **Health Check Configuration:** The `docker-compose.yml` file specifies a health check for the `django-backend` service that points to a `/health/` endpoint. This endpoint does not exist yet, causing the health check to fail initially. This highlights the need to implement a dedicated health check endpoint as a priority.
-   **Environment Variable Loading:** Ensuring that all necessary environment variables are correctly passed from the `.env` file to the Docker container and are available to the Django settings required careful configuration.

### Trade-offs Made
-   **Development Velocity vs. Immediate Robustness:** The project was initialized with a minimal set of features to accelerate the setup process. Features like comprehensive tests and production-ready logging were deprioritized in favor of quickly establishing a working development environment.
-   **Simplicity vs. Feature-richness:** The initial setup uses a simple structure. As the project grows, it will need to be refactored into smaller, more manageable Django apps.

## 4. Future Work & Frontend

### What I Would Add With More Time
-   **Implement Core API Endpoints:** Add full CRUD (Create, Read, Update, Delete) functionality for tasks.
-   **Add User Authentication:** Secure the API using JWT (JSON Web Tokens) for stateless authentication.
-   **Implement Health Check Endpoint:** Create a `/health/` view to satisfy the Docker health check and for monitoring purposes.
-   **Set Up a Test Suite:** Configure `pytest-django` and write unit and integration tests for the API.
-   **Enable and Configure Redis/Celery:** For handling background tasks such as sending email notifications.
-   **CI/CD Pipeline:** Set up a continuous integration and deployment pipeline.

### Justification for Using Django Templates for the Frontend
The current project is configured as a **headless REST API** and is **not using Django Templates for the frontend**. The `TEMPLATES` engine is enabled in `settings.py`, but this is a default Django setting required for features like the built-in admin interface (`/admin/`) and for rendering error pages.

The architectural decision is to have a **decoupled frontend** (e.g., a Single Page Application built with React, Vue, or Angular) that communicates with this Django backend via the REST API. This approach provides a clear separation of concerns between the frontend and backend, allowing them to be developed, deployed, and scaled independently.
