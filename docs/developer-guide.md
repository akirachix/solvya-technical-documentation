# Developer Guide

## 1. Introduction

This guide introduces the development environment and project structure used to develop and maintain Waliin.

Waliin consists of a Next.js frontend and a FastAPI backend, with PostgreSQL as its primary database.

## 2. Development Prerequisites

The development environment requires the following tools:

| Tool | Purpose |
|---|---|
| Python 3.11+ | Backend development |
| Node.js | Frontend development |
| npm | Frontend package management |
| PostgreSQL | Relational database |
| Git | Source code version control |
| Visual Studio Code | Code editing |

## 3. Project Structure

Waliin is maintained in separate frontend and backend projects.

### 3.1 Frontend

The frontend uses Next.js, React and TypeScript.

Important directories include:

- `app/` — application routes and pages.
- `components/` — reusable interface components.
- `lib/` — API client, authentication and application utilities.
- `public/` — static assets.

### 3.2 Backend

The backend uses FastAPI and Python.

Its main application entry point is `main.py`. The application registers routers for authentication, users, equipment, faults, assessments, repairs, verification and reports.

## 4. Development Workflow

A typical development workflow includes:

1. Review the relevant feature and its requirements.
2. Identify whether the change belongs to the frontend or backend.
3. Implement the change in the appropriate project.
4. Check API compatibility between frontend and backend.
5. Run the relevant tests and quality checks.
6. Review the resulting application behaviour.
7. Update technical documentation when necessary.

## 5. Backend Development Setup

The backend project uses Python and FastAPI.

A typical local setup involves:

1. Open the backend project directory.
2. Create and activate a Python virtual environment.
3. Install the dependencies listed in the project's dependency file.
4. Configure the required application environment variables.
5. Ensure PostgreSQL is available and configured.
6. Apply database migrations using Alembic.
7. Start the FastAPI development server.

The backend application entry point is `main.py`.

## 6. Frontend Development Setup

The frontend project uses Next.js and npm.

A typical local setup involves:

1. Open the frontend project directory.
2. Install dependencies using `npm install`.
3. Configure the backend URL where required.
4. Start the Next.js development server using `npm run dev`.

The frontend development server runs using the Next.js development command.

## 7. Testing and Quality Checks

The frontend project provides the following scripts:

| Command | Purpose |
|---|---|
| `npm run dev` | Start the development server |
| `npm run build` | Build the frontend |
| `npm run lint` | Run ESLint |
| `npm run test` | Run Vitest tests |
| `npm run format:check` | Check code formatting |
| `npm run format` | Format project files |

The backend project uses pytest for automated tests and Ruff for Python code quality checks.

## 8. Database Migrations

Waliin uses Alembic to manage database schema changes.

Database migrations should be maintained as versioned migration files so that database structure changes can be applied consistently across environments.

## 9. Development Best Practices

- Keep frontend and backend responsibilities separate.
- Reuse existing API client and authentication utilities.
- Validate incoming API data.
- Keep database schema changes in migrations.
- Write tests for new functionality.
- Avoid committing environment files or credentials.
- Update documentation when application behaviour changes.

## 10. Related Documentation

- [System Architecture](architecture.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [Database Design](database-design.md)
- [Testing](testing.md)