
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

The main application registers 14 router groups using `app.include_router()`.

The registered router groups cover:

1. Authentication
2. Users
3. Dashboard
4. Equipment
5. Priority List
6. Fault Assessments
7. Repair Verification Records
8. Maintenance Reports
9. Repair Work
10. Fault Management
11. Notifications
12. Resource Requests
13. Request Items
14. Request Follow-ups

Each router groups related endpoints and delegates application operations to the relevant service and repository components.

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

The backend exposes its functionality through 14 registered router groups.

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

### 6.11 Notifications API

Router prefix: `/notifications`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/notifications/` | Create a notification |
| GET | `/notifications/` | List notifications for the authenticated user |
| GET | `/notifications/me` | Retrieve the authenticated user's notifications |
| GET | `/notifications/{id}` | Retrieve a specific notification |
| POST | `/notifications/{id}/read` | Mark a notification as read |

The notification router uses `NotificationService` for notification operations.

The router uses the `get_current_user` dependency to identify the authenticated user. Notification retrieval and read operations are scoped to that user.

The create endpoint returns HTTP 201 when a notification is created.

### 6.12 Resource Requests API

The resource requests router does not declare an explicit prefix.

| Method | Endpoint | Description |
|---|---|---|
| POST | `/requests` | Create a resource request |
| GET | `/requests` | List resource requests |
| GET | `/requests/overdue` | Retrieve overdue requests |
| GET | `/requests/{request_id}` | Retrieve a specific request |
| PATCH | `/requests/{request_id}` | Update a resource request |
| POST | `/requests/{request_id}/decide` | Record a manager's decision on a request |

The router delegates operations to `resource_requests_service`.

The request creation endpoint accepts a `ResourceRequestsCreate` payload.

The update endpoint accepts a `ResourceRequestsUpdate` payload, while the decision endpoint accepts a `ResourceRequestsDecide` payload.

The decision endpoint reads `x_user_role` and `user_id` from request headers and delegates the decision operation to the service layer.

### 6.13 Request Items API

The request items router manages individual items associated with resource requests.

| Method | Endpoint | Description |
|---|---|---|
| GET | `/requests/{request_id}/items` | Retrieve items belonging to a request |
| PATCH | `/requests/{request_id}/items/{item_id}` | Update the fulfilled quantity of a request item |

The router delegates operations to the request items service.

The GET endpoint returns a list of `RequestItemsResponse` objects.

The PATCH endpoint accepts an optional `quantity_fulfilled` query parameter and returns the updated request item.

### 6.14 Request Follow-ups API

The request follow-ups router supports communication and follow-up records associated with resource requests.

| Method | Endpoint | Description |
|---|---|---|
| POST | `/requests/{request_id}/follow-ups` | Create a follow-up record |
| GET | `/requests/{request_id}/follow-ups` | Retrieve follow-ups for a request |
| POST | `/follow-ups/{follow_up_id}/reply` | Record a reply to a follow-up |
| PATCH | `/follow-ups/{follow_up_id}` | Update a follow-up record |

The router delegates operations to `request_follow_ups_service`.

The creation endpoint accepts a `RequestFollowUpsCreate` payload and returns HTTP 201.

The reply endpoint accepts a `RequestFollowUpsReply` payload, while the update endpoint accepts a `RequestFollowUpsUpdate` payload.

The follow-up creation endpoint reads the user role and user ID from request headers.

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

The backend implements several controls to protect user authentication and session information.

These include:

- **Password hashing:** Argon2 is used to hash user passwords.
- **Multi-factor authentication:** The backend supports six-digit TOTP verification.
- **MFA secret encryption:** Stored MFA secrets are encrypted using AES-256-GCM.
- **Session-token protection:** Session tokens are stored as hashes rather than plaintext values.
- **Login-attempt limiting:** The login flow implements an attempt limiter to restrict repeated authentication attempts.

The MFA encryption key is supplied through application configuration.

The login-attempt limiter is maintained in application memory. Its state does not persist across server restarts and should not be described as a distributed rate-limiting mechanism.

## 8. Environment Configuration

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

## 11. Summary

The Waliin backend provides a FastAPI-based REST API for managing medical equipment lifecycles in Ethiopian hospitals.

Its 14 registered router groups cover authentication, user management, equipment registration, fault reporting and assessment, prioritisation, repair operations, verification records, maintenance reporting, notifications and resource request workflows.

The layered architecture separates routing, validation, business logic and database access. SQLAlchemy and PostgreSQL support data persistence, while Alembic manages database schema migrations.

Authentication and security controls include Argon2 password hashing, multi-factor authentication, encrypted MFA secrets and session management.

## Backend Resources

The following resource provides access to the deployed Waliin backend API documentation.

### Interactive API Documentation

The backend exposes interactive API documentation through Swagger UI. It provides an interface for exploring the available API endpoints and their request and response schemas.

[Open Waliin Backend API Documentation](https://waliin-8c96dd4bd190.herokuapp.com/docs)
