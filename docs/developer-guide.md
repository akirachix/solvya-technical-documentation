
# Developer Guide

## 1. Introduction

This guide introduces the development environment, project structure and workflows used to develop and maintain Waliin.

Waliin consists of a Next.js frontend and a FastAPI backend, with PostgreSQL as its primary database.

The frontend communicates with the backend through HTTP API requests, while the backend handles application logic, authentication, authorization and database operations.

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

Developers should also have access to the project repositories and the required application configuration values.

## 3. Project Structure

Waliin is maintained in separate frontend and backend projects.

### 3.1 Frontend

The frontend uses Next.js, React and TypeScript.

Important directories include:

- `app/` — application routes and pages.
- `components/` — reusable interface components.
- `lib/` — API client, authentication and application utilities.
- `public/` — static assets.

The frontend uses the Next.js App Router to organize application pages and navigation.

### 3.2 Backend

The backend uses FastAPI and Python.

Its main application entry point is `main.py`.

The application registers router groups for:

- Authentication.
- User management.
- Dashboard.
- Equipment management.
- Priority lists.
- Fault assessment.
- Repair verification records.
- Maintenance reports.
- Repair work.
- Fault management.
- Notifications.
- Resource requests.
- Request items.
- Request follow-ups.

The backend separates routing, validation, business logic, database access and storage responsibilities.

## 4. Development Workflow

A typical development workflow includes:

1. Review the relevant feature and its requirements.
2. Identify whether the change belongs to the frontend or backend.
3. Implement the change in the appropriate project.
4. Check API compatibility between frontend and backend.
5. Run the relevant tests and quality checks.
6. Review the resulting application behaviour.
7. Update technical documentation when necessary.

Changes affecting both frontend and backend should be checked together to ensure that API contracts remain consistent.

## 5. Backend Development Setup

The backend project uses Python, FastAPI and PostgreSQL.

### 5.1 Open the Backend Project

Navigate to the backend repository:

```bash
cd /path/to/solvya-backend
```

### 5.2 Create a Virtual Environment

Using Python's virtual environment module:

```bash
python3 -m venv .venv
```

Activate the environment on Linux:

```bash
source .venv/bin/activate
```

Alternatively, the project can use `uv` for environment and dependency management.

### 5.3 Install Dependencies

If the project uses `uv`:

```bash
uv sync
```

If dependencies are managed through `requirements.txt`:

```bash
pip install -r requirements.txt
```

Use the dependency management method configured in the backend repository.

### 5.4 Configure Environment Variables

Configure the application environment using the required environment variables.

These may include:

- Database connection settings.
- Session configuration.
- MFA encryption settings.
- Frontend and dashboard URLs.
- Email backend configuration.

Do not commit `.env` files, passwords, encryption keys or other secrets to source control.

### 5.5 Apply Database Migrations

Apply the database migrations using Alembic:

```bash
uv run alembic upgrade head
```

### 5.6 Start the Backend Server

Start the FastAPI development server:

```bash
uv run uvicorn main:app --reload
```

The local API documentation is available at:

```text
http://127.0.0.1:8000/docs
```

## 6. Frontend Development Setup

The frontend project uses Next.js, React, TypeScript and npm.

### 6.1 Open the Frontend Project

Navigate to the frontend repository:

```bash
cd /path/to/solvya-frontend
```

### 6.2 Install Dependencies

```bash
npm install
```

### 6.3 Configure Backend Connectivity

Configure the backend URL and API prefix using the environment variables supported by the frontend:

- `BACKEND_URL`
- `BACKEND_API_PREFIX`

Ensure that the frontend can reach the running FastAPI backend.

### 6.4 Start the Frontend Server

```bash
npm run dev
```

The Next.js development server provides the local frontend application.

## 7. Testing and Quality Checks

### 7.1 Frontend Commands

The frontend project provides the following scripts:

| Command | Purpose |
|---|---|
| `npm run dev` | Start the development server |
| `npm run build` | Build the frontend |
| `npm run start` | Start the production server |
| `npm run lint` | Run ESLint |
| `npm run test` | Run Vitest tests |
| `npm run format:check` | Check code formatting |
| `npm run format` | Format project files |

### 7.2 Backend Commands

The backend uses pytest for automated tests and Ruff for Python code quality checks.

Run the backend tests:

```bash
uv run pytest -q
```

Run Ruff checks:

```bash
uv run ruff check .
```

The commands should be executed from the backend project directory with the appropriate dependencies installed.

## 8. Database Migrations

Waliin uses Alembic to manage database schema changes.

Database migrations should be maintained as versioned migration files so that database structure changes can be applied consistently across environments.

Common migration commands include:

**Apply migrations:**

```bash
uv run alembic upgrade head
```

**View the current migration revision:**

```bash
uv run alembic current
```

**View migration history:**

```bash
uv run alembic history
```

**Generate a migration from model changes:**

```bash
uv run alembic revision --autogenerate -m "Describe schema change"
```

Generated migrations should be reviewed before being applied. Developers should verify that the migration correctly represents the intended schema changes.

Previously applied migrations should not be edited to introduce new schema changes. Create a new migration revision instead.

## 9. Version Control

Git is used to manage source code changes.

A typical workflow includes:

1. Check the current branch and working tree.
2. Create or switch to the appropriate feature branch.
3. Implement and test the changes.
4. Review the changes before committing.
5. Commit the completed work.
6. Push the branch to the remote repository.
7. Open a pull request for review.

Useful Git commands include:

```bash
git status
git branch --show-current
git diff
git diff --check
```

Only commit files related to the intended change. Avoid committing generated build directories, local environment files and application secrets.

## 10. Development Best Practices

- Keep frontend and backend responsibilities separate.
- Reuse existing API client and authentication utilities.
- Validate incoming API data.
- Enforce authorization in the backend.
- Keep database schema changes in Alembic migrations.
- Write tests for new functionality.
- Avoid committing environment files or credentials.
- Use descriptive Git commit messages.
- Review changes before pushing them.
- Update documentation when application behaviour changes.

## 11. Related Documentation

- [System Architecture](architecture.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [API Reference](api-reference.md)
- [Database Design](database-design.md)
- [Authentication and Security](authentication-and-security.md)
- [Deployment Guide](deployment-guide.md)
- [Testing](testing.md)
