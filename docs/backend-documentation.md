# Backend Documentation

## 1. Introduction

The Waliin backend is a REST API built with FastAPI. It supports the management and tracking of medical equipment lifecycles in Ethiopian hospitals.

The backend provides functionality for user authentication, equipment registration and approval, fault reporting, fault assessment, repair management, maintenance reporting and dashboard summaries.

**Application details**

| Property | Value |
|---|---|
| Application name | Waliin |
| Version | 0.1.0 |
| Framework | FastAPI |
| Language | Python 3.11+ |
| Database ORM | SQLAlchemy |
| Database | PostgreSQL |
| API style | REST |

## 2. Backend Architecture

The backend follows a layered architecture that separates API routing, data validation, business logic and database operations.

### 2.1 Main components

| Component | Responsibility |
|---|---|
| `routers/` | Defines API endpoints and handles HTTP requests. |
| `schemas/` | Defines request validation and response structures using Pydantic. |
| `services/` | Implements application and business logic. |
| `repositories/` | Handles database access and persistence operations. |
| `models/` | Defines SQLAlchemy database models. |
| `security/` | Contains authentication and security-related functionality. |
| `alembic/` | Manages database schema migrations. |
| `tests/` | Contains automated backend tests. |
| `templates/` | Contains email templates. |

### 2.2 Request processing

A typical request follows this flow:

1. A client sends an HTTP request to an API endpoint.
2. The corresponding router receives the request.
3. Pydantic schemas validate incoming data and define response structures.
4. The service layer processes the business operation.
5. Repository and model components support database operations.
6. The router returns the appropriate response to the client.

## 3. Technology Stack

The backend uses the following technologies and libraries:

| Technology | Purpose |
|---|---|
| Python | Backend programming language |
| FastAPI | REST API framework |
| Uvicorn | ASGI application server |
| SQLAlchemy | ORM and database interaction |
| PostgreSQL | Relational database |
| Psycopg | PostgreSQL connectivity |
| Pydantic | Data validation and serialization |
| Pydantic Settings | Application configuration |
| Alembic | Database migrations |
| PyJWT | JWT-related functionality |
| pwdlib with Argon2 | Password hashing |
| Redis | Redis integration support |
| Cryptography | Cryptographic operations |
| ReportLab | PDF generation |
| python-multipart | Multipart form and file uploads |
| pytest | Automated testing |
| Ruff | Python linting and formatting |

## 4. Application Configuration

The main application is initialized in `main.py`.

It defines the FastAPI application with the following metadata:

- Title: Waliin
- Version: 0.1.0
- Description: Backend API for tracking medical equipment lifecycles in Ethiopian hospitals.

### 4.1 Registered routers

The following ten routers are registered using `app.include_router()`:

1. Authentication
2. Users
3. Dashboard
4. Equipment
5. Priority list
6. Fault assessments
7. Repair verification records
8. Maintenance reports
9. Repair work
10. Fault management

The application also exposes a health-check endpoint:

| Method | Endpoint | Response |
|---|---|---|
| GET | `/health` | `{"status": "ok"}` |

### 4.2 Error handling

The application implements a custom exception handler for `ServiceError`.

The handler returns a JSON response containing the error message:

`{"detail": error.message}`

The HTTP status code is taken from the exception's `status_code` property.

## 5. Database Integration

Database connectivity is configured in `database.py`.

The backend uses SQLAlchemy to interact with PostgreSQL.

### 5.1 Database session management

The database module:

- Loads environment variables using `python-dotenv`.
- Reads the database connection string from `DATABASE_URL`.
- Creates a SQLAlchemy engine when the database URL is available.
- Configures `SessionLocal` for database sessions.
- Defines the declarative `Base` used by ORM models.
- Provides a `get_db()` dependency for database session management.

The `get_db()` function creates a session, yields it to the requesting operation and closes it in a `finally` block.

### 5.2 Database migrations

Alembic manages database schema migrations.

The migration configuration is stored in `alembic.ini`, while migration environment configuration is defined in `alembic/env.py`.

The migration environment imports the application's SQLAlchemy metadata and supports online and offline migration execution.

## 6. API Documentation

The backend exposes its functionality through ten registered router modules.

The paths below are the router paths declared in the application. No additional global API prefix is declared in `main.py`.

### 6.1 Authentication API

Router prefix: `/auth`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/auth/login` | Authenticate a user |
| POST | `/auth/logout` | Log out a user |
| GET | `/auth/me` | Retrieve the current user |
| POST | `/auth/mfa/setup` | Set up multi-factor authentication |
| POST | `/auth/mfa/confirm` | Confirm MFA setup |
| POST | `/auth/mfa/verify` | Verify an MFA challenge |
| POST | `/auth/accept-invite` | Accept a user invitation |
| POST | `/auth/forgot-password` | Initiate password recovery |
| POST | `/auth/reset-password` | Reset a user's password |

### 6.2 User Management API

Router prefix: `/users`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/users` | Create a user |
| GET | `/users` | List users |
| PATCH | `/users/{user_id}` | Update a user |
| POST | `/users/{user_id}/resend-invite` | Resend an invitation |
| POST | `/users/{user_id}/revoke` | Revoke a user |
| POST | `/users/{user_id}/send-reset-link` | Send a password reset link |

### 6.3 Dashboard API

Router prefix: `/dashboard`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/dashboard/summary` | Retrieve dashboard summary data |

The endpoint delegates summary generation to `DashboardService` and returns a `DashboardSummary` response.

### 6.4 Equipment Management API

Router prefix: `/equipment`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/equipment/departments` | Create a department |
| GET | `/equipment/departments` | List departments |
| DELETE | `/equipment/documents/{doc_id}` | Delete an equipment document |
| GET | `/equipment/departments/{department_id}` | Retrieve a department |
| PATCH | `/equipment/departments/{department_id}` | Update a department |
| PATCH | `/equipment/departments/{department_id}/deactivate` | Deactivate a department |
| POST | `/equipment` | Register equipment |
| GET | `/equipment` | List equipment |
| GET | `/equipment/pending` | List pending equipment |
| GET | `/equipment/out-of-service` | List out-of-service equipment |
| GET | `/equipment/mine` | List equipment belonging to the current engineer |
| POST | `/equipment/{equipment_id}/resubmit` | Resubmit equipment |
| GET | `/equipment/{equipment_id}` | Retrieve equipment details |
| PATCH | `/equipment/{equipment_id}` | Update equipment |
| POST | `/equipment/{equipment_id}/approve` | Approve equipment |
| POST | `/equipment/{equipment_id}/return` | Return equipment |
| POST | `/equipment/{equipment_id}/documents` | Upload an equipment document |
| GET | `/equipment/documents/{doc_id}/download` | Download an equipment document |
| POST | `/equipment/import-csv` | Import equipment using CSV |

The equipment router delegates operations to the equipment service and associated repositories.

It supports multipart file uploads for equipment documents and CSV imports.

### 6.5 Fault Management API

Router prefix: `/faults`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/` | Report a fault |
| GET | `/faults/` | List faults |
| GET | `/faults/{fault_id}` | Retrieve fault details |
| POST | `/faults/{fault_id}/assign` | Assign a fault |
| POST | `/faults/{fault_id}/status` | Update fault status |
| POST | `/faults/{fault_id}/close` | Close a fault |

### 6.6 Fault Assessment API

Router prefix: `/faults`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/{fault_id}/assessments` | Create a fault assessment |
| GET | `/faults/{fault_id}/assessments` | Retrieve assessments for a fault |

The router uses `AssessmentService` and returns `FaultAssessmentRead` response objects.

The currently registered router uses an engineer dependency that reads the engineer UUID from the `X-Engineer-Id` header.

### 6.7 Priority List API

Router prefix: `/faults`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/faults/priority-list` | Retrieve the prioritised fault list |

The endpoint uses `PriorityListService` and returns a list of `PriorityListItem` objects.

### 6.8 Repair Verification Records API

Router prefix: `/repair-verification-records`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/repair-verification-records/` | Create a verification record |
| GET | `/repair-verification-records/` | List verification records |
| GET | `/repair-verification-records/{record_id}` | Retrieve a verification record |
| PUT | `/repair-verification-records/{record_id}` | Update a verification record |
| DELETE | `/repair-verification-records/{record_id}` | Delete a verification record |

The router delegates operations to the repair verification record service.

Its handlers declare a required UUID `user_id` header. The current handlers pass database sessions and relevant payloads to the service functions.

### 6.9 Repair Work API

This router does not declare an explicit prefix.

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/{fault_id}/repairs` | Record repair work |
| POST | `/faults/{fault_id}/tests` | Record repair testing |
| POST | `/faults/{fault_id}/release` | Release a fault |
| GET | `/faults/{fault_id}/records` | Retrieve repair records |

The router delegates operations to `services.repair_work`.

The first three endpoints declare a required UUID `user_id` header. The records endpoint does not declare this header.

### 6.10 Maintenance Reports API

Router prefix: `/reports`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/reports/maintenance-summary` | Retrieve maintenance summary data |
| GET | `/reports/maintenance-summary/pdf` | Generate and download a maintenance summary PDF |

The endpoints use `MaintenanceReportService`.

The summary endpoint returns `MaintenanceReportSummary`.

The PDF endpoint returns a `StreamingResponse` with the media type `application/pdf`. The generated file is named `waliin-maintenance-report.pdf`.

## 7. Authentication and Authorization

The backend implements session-based authentication.

### 7.1 Session management

The session configuration includes:

- Session cookie name: `__Host-waliin_session`
- Cookie security: Secure
- HTTP-only: Enabled
- SameSite policy: Strict
- Cookie path: `/`
- Session idle timeout: 15 minutes
- Maximum session duration: 8 hours

The current session dependency reads the session cookie and validates the session.

Inactive accounts have their sessions ended. The current-user dependency also checks whether MFA verification has been completed.

### 7.2 User roles

The backend defines three user roles:

- `clinical_staff`
- `biomedical_engineer`
- `health_manager`

Role-based dependencies restrict access to operations according to the required role.

### 7.3 Password and MFA security

The implementation uses Argon2 password hashing.

MFA-related functionality includes setup, confirmation and verification endpoints. The application configuration also provides an MFA encryption key setting.

## 8. Application Configuration

Application settings are managed through `config.py` using Pydantic Settings.

The configuration supports:

- Application environment settings
- Session duration and cookie configuration
- Redis connection settings
- MFA encryption and issuer settings
- Frontend and dashboard base URLs
- Email backend selection
- SMTP server configuration
- Email sender configuration

Environment variables are loaded from `.env` when available.

Configuration values and defaults do not, by themselves, establish that an external service such as Redis or SMTP is active in a particular deployment.

## 9. Testing and Code Quality

The backend uses pytest for automated testing.

The test directory is organised into:

- `auth_tests/`
- `equipment_tests/`
- `model_tests/`
- `security_tests/`
- `session_tests/`

The project also includes:

- Ruff for linting and formatting
- pytest-cov for test coverage reporting

The project configuration specifies Python 3.11 as the Ruff target and uses an 88-character line length.

## 10. Deployment

The backend includes a `Procfile` defining its web process:

`web: uvicorn main:app --host 0.0.0.0 --port $PORT`

The project README documents deployment using Heroku and CI workflows.

Production configuration values, including database connection and security settings, should be supplied through the deployment environment rather than committed to source control.

## 11. Unregistered Router Modules

The backend repository also contains the following router modules:

- `notification.py`
- `request_follow_ups.py`
- `request_items.py`
- `resource_requests.py`

These files exist in the routers directory but are not included through `app.include_router()` in the inspected `main.py`.

They are therefore excluded from the list of active application routes in this documentation.

## 12. Summary

The Waliin backend provides a FastAPI-based service for managing medical equipment lifecycles.

Its registered API modules cover authentication, user management, equipment management, fault reporting and assessment, repair operations, verification records, maintenance reports, prioritised faults and dashboard summaries.

The layered architecture separates routing, validation, business logic and database access, while SQLAlchemy and Alembic support persistence and schema management.

## Backend Resources

The following resource provides access to the deployed Waliin backend API documentation.

### Interactive API Documentation

The backend exposes interactive API documentation through Swagger UI. It provides an interface for exploring the available API endpoints and their request and response schemas.

[Open Waliin Backend API Documentation](https://waliin-8c96dd4bd190.herokuapp.com/docs)