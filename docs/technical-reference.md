
# Technical Reference

## 1. Introduction

This document provides a high-level technical reference for Waliin, covering its application technologies and the main technical components used across the system.

It serves as a quick reference to the technologies and supporting documentation for the frontend, backend, API, database, development, testing and deployment.

For detailed implementation information, refer to the corresponding technical documents listed in this reference.

## 2. Technology Stack

Waliin uses the following technologies across its application layers:

| Layer | Technology | Purpose |
|---|---|---|
| Frontend framework | Next.js 16.4.3 | Web application framework |
| UI library | React 19.3.0 | User interface development |
| Frontend language | TypeScript | Frontend development |
| Backend framework | FastAPI | Backend API development |
| Backend language | Python 3.11+ | Backend implementation |
| Database | PostgreSQL | Persistent data storage |
| ORM | SQLAlchemy | Database integration |
| Migration tool | Alembic | Database schema migrations |
| Data validation | Pydantic | Request and configuration validation |
| Frontend testing | Vitest | Automated frontend testing |
| Backend testing | pytest | Automated backend testing |
| Code quality | ESLint and Ruff | Code quality checks |

## 3. Frontend Technical Overview

The frontend uses Next.js App Router, React and TypeScript.

Its main technical components include:

- Application routes and page components.
- Reusable interface components.
- Shared authentication utilities.
- API client for backend communication.
- Static application assets.

The shared API client is implemented in `lib/api/client.ts`, with `apiFetch<T>()` handling API requests and HTTP responses.

For detailed information about frontend structure, routes, components, authentication integration and styling, refer to the [Frontend Documentation](frontend-documentation.md).

## 4. Backend Technical Overview

The backend is implemented using FastAPI and Python.

The main application entry point is `main.py`, which initializes the application and registers the API routers.

Important backend technologies include:

- SQLAlchemy for database integration.
- Alembic for database migrations.
- Pydantic for data validation.
- PyJWT for token-related functionality.
- Argon2 through `pwdlib` for password hashing.
- Redis for integration support.
- ReportLab for PDF generation.

The backend uses a layered structure that separates HTTP routing, request validation, application logic, database access and data representation.

For detailed information about backend architecture, application structure, configuration, request processing and error handling, refer to the [Backend Documentation](backend-documentation.md).

## 5. API Reference

The backend exposes HTTP endpoints through registered FastAPI routers.

The API provides functionality for:

- Authentication and user management.
- Dashboard information.
- Equipment management.
- Fault reporting and assessment.
- Equipment prioritisation.
- Repair verification.
- Maintenance reporting.
- Notifications.
- Resource requests and follow-ups.

For individual endpoints, HTTP methods, request parameters, response details and API usage, refer to the [API Reference](api-reference.md).

## 6. Database Reference

Waliin uses PostgreSQL with SQLAlchemy and Alembic.

The database implementation includes:

- Relational tables for application entities.
- Primary and foreign key relationships.
- Database constraints and indexes.
- Database triggers.
- A fault downtime view.
- Versioned database migrations.

For detailed schema information, table definitions, relationships, constraints and migration details, refer to the [Database Design](database-design.md).

## 7. Authentication and Security

The application includes authentication and security functionality to support user access and protect application resources.

The main security areas include:

- User authentication.
- Session management.
- Password hashing.
- Multi-factor authentication.
- Role-based access control.
- Login attempt protection.

For detailed authentication flows, session configuration, security mechanisms and access restrictions, refer to [Authentication and Security](authentication-and-security.md).

## 8. Equipment Prioritisation

Waliin uses a rule-based approach to equipment prioritisation during the pilot.

Prioritisation considers recorded equipment condition, inspection findings, fault status, maintenance history, clinical criticality, backup availability and biomedical engineer assessments.

AI and machine learning-based predictive failure analysis are outside the scope of the pilot.

For information about the application workflows and backend implementation, refer to the [Frontend Documentation](frontend-documentation.md), [Backend Documentation](backend-documentation.md) and [API Reference](api-reference.md).

## 9. Configuration and Deployment

The frontend and backend use environment-based configuration to manage application settings and service connectivity.

### 9.1 Frontend Configuration

Frontend configuration includes:

- `BACKEND_URL`
- `BACKEND_API_PREFIX`

### 9.2 Backend Configuration

Backend configuration includes:

- Database connectivity.
- Session settings.
- MFA configuration.
- Frontend and dashboard base URLs.
- Email and other application service settings.

Sensitive configuration values should be supplied through the appropriate environment configuration and must not be committed to source control.

For environment configuration, deployment architecture, hosting information and maintenance considerations, refer to the [Deployment Guide](deployment-guide.md).

## 10. Development and Testing Reference

Waliin has separate frontend and backend development environments.

The frontend uses npm scripts for development, production builds, testing, linting and formatting.

The backend uses Python tooling for dependency management, application execution, automated testing and code-quality checks.

For local development setup and development workflows, refer to the [Developer Guide](developer-guide.md).

For testing tools, test execution commands, functional testing scope and test reporting, refer to the [Testing](testing.md) document.

## 11. Related Documentation

The following documents provide detailed information about specific areas of Waliin:

| Documentation | Description |
|---|---|
| [Project Overview](overview.md) | Project purpose, objectives and application summary. |
| [Problem Exploration](problem-exploration.md) | Healthcare equipment management challenges and proposed solution. |
| [System Architecture](architecture.md) | System components, architecture diagrams and interactions. |
| [Frontend Documentation](frontend-documentation.md) | Frontend structure, routes, components and API integration. |
| [Backend Documentation](backend-documentation.md) | Backend structure, services, repositories and implementation. |
| [API Reference](api-reference.md) | API endpoints, methods and request and response details. |
| [Database Design](database-design.md) | Database entities, relationships and schema structure. |
| [Authentication and Security](authentication-and-security.md) | Authentication, sessions and security controls. |
| [Developer Guide](developer-guide.md) | Local development setup and development workflows. |
| [Testing](testing.md) | Testing approach, tools and verification procedures. |
| [Deployment Guide](deployment-guide.md) | Deployment architecture and configuration. |
| [Glossary](glossary.md) | Definitions of technical and application-specific terms. |
