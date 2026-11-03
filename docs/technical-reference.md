# Technical Reference

## 1. Introduction

This document provides a technical reference for Waliin, covering its application technologies, backend components, frontend dependencies, configuration and technical conventions.

## 2. Technology Stack

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

## 3. Frontend Technical Components

The Waliin frontend uses Next.js App Router and organizes application functionality into routes and reusable components.

### 3.1 Important directories

| Directory | Responsibility |
|---|---|
| `app/` | Application routes and pages |
| `components/` | Reusable interface components |
| `lib/` | API client, authentication and utility functions |
| `public/` | Static assets |

### 3.2 Frontend API communication

The frontend uses a shared API client in `lib/api/client.ts`.

The `apiFetch` function:

- Sends requests to the `/api` route.
- Includes browser credentials.
- Uses JSON request headers.
- Parses JSON responses.
- Handles HTTP errors through `ApiError`.
- Handles responses with no content.

## 4. Backend Technical Components

The backend is implemented using FastAPI.

The main application entry point is `main.py`, which initializes the application and registers the API routers.

Important backend technologies include:

- SQLAlchemy for database integration.
- Alembic for database migrations.
- Pydantic for data validation.
- PyJWT for token-related functionality.
- Argon2 through `pwdlib` for password hashing.
- Redis as a configured dependency.
- ReportLab for PDF generation.

## 5. API Reference

The backend exposes HTTP endpoints through registered FastAPI routers.

The main API groups include:

| API group | Base path | Responsibility |
|---|---|---|
| Authentication | `/auth` | Login, logout and authentication |
| Users | `/users` | User account management |
| Dashboard | `/dashboard` | Dashboard summary |
| Equipment | `/equipment` | Equipment and department management |
| Faults | `/faults` | Fault reporting and management |
| Assessments | `/faults` | Technical fault assessments |
| Priority list | `/faults` | Fault prioritization |
| Repair verification | `/repair-verification-records` | Repair verification records |
| Maintenance reports | `/reports` | Maintenance summaries |
| Repair work | `/faults` | Repair and testing operations |

See [API Reference](api-reference.md) for individual endpoints and HTTP methods.

## 6. Frontend Configuration

The frontend uses the following environment variables:

| Variable | Purpose |
|---|---|
| `BACKEND_URL` | Backend server address |
| `BACKEND_API_PREFIX` | Backend API prefix; defaults to `/api/v1` |

The Next.js configuration uses these values to configure API request rewrites when a backend URL is provided.

## 7. Database Reference

Waliin uses PostgreSQL with SQLAlchemy and Alembic.

The database implementation includes:

- Relational tables for application entities.
- Primary and foreign key relationships.
- Database constraints and indexes.
- Database triggers.
- A fault downtime view.
- Versioned database migrations.

See [Database Design](database-design.md) for the detailed schema.

## 8. Error Handling

The backend uses a centralized `ServiceError` exception handler.

Service errors are returned as JSON responses containing a `detail` field and the configured HTTP status code.

The frontend API client uses an `ApiError` class to represent HTTP errors and their status codes.

## 9. Testing and Development Commands

The frontend defines these npm scripts:

| Command | Purpose |
|---|---|
| `npm run dev` | Start development server |
| `npm run build` | Build the application |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run test` | Run Vitest |
| `npm run format:check` | Check formatting |

The backend uses pytest for automated tests and Ruff for code quality.

## 10. Related Documentation

- [System Architecture](architecture.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [API Reference](api-reference.md)
- [Database Design](database-design.md)
- [Developer Guide](developer-guide.md)
- [Testing](testing.md)