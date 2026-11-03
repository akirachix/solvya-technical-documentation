# API Reference

## 1. Introduction

This document describes the HTTP API endpoints registered by the Waliin FastAPI backend.

The API supports authentication, user management, equipment management, fault reporting, technical assessments, repair verification and maintenance reporting.

## 2. API Information

| Property | Value |
|---|---|
| Application | Waliin API |
| Framework | FastAPI |
| API version | 0.1.0 |
| Data format | JSON |
| Health endpoint | `/health` |

The backend routers are registered in `main.py`.

The frontend can use `BACKEND_API_PREFIX` to configure the API prefix. The documented backend routes below are the paths declared by the FastAPI routers.

## 3. Authentication Endpoints

Base path: `/auth`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/auth/login` | Authenticate a user |
| POST | `/auth/logout` | End the authenticated session |
| GET | `/auth/me` | Retrieve the current authenticated user |
| POST | `/auth/mfa/setup` | Begin multi-factor authentication setup |
| POST | `/auth/mfa/confirm` | Confirm multi-factor authentication setup |
| POST | `/auth/mfa/verify` | Verify multi-factor authentication |
| POST | `/auth/accept-invite` | Accept a user invitation |
| POST | `/auth/forgot-password` | Request a password reset |
| POST | `/auth/reset-password` | Complete a password reset |

## 4. User Management Endpoints

Base path: `/users`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/users` | Create a user |
| GET | `/users` | Retrieve users |
| PATCH | `/users/{user_id}` | Update a user |
| POST | `/users/{user_id}/resend-invite` | Resend a user invitation |
| POST | `/users/{user_id}/revoke` | Revoke a user |
| POST | `/users/{user_id}/send-reset-link` | Send a password reset link |

## 5. Equipment Management Endpoints

Base path: `/equipment`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/equipment/departments` | Create a department |
| GET | `/equipment/departments` | List departments |
| GET | `/equipment/departments/{department_id}` | Retrieve a department |
| PATCH | `/equipment/departments/{department_id}` | Update a department |
| DELETE | `/equipment/departments/{department_id}` | Deactivate a department |
| PATCH | `/equipment/departments/{department_id}/deactivate` | Deactivate a department |
| POST | `/equipment` | Register equipment |
| GET | `/equipment` | List equipment |
| GET | `/equipment/pending` | List pending equipment |
| GET | `/equipment/out-of-service` | List out-of-service equipment |
| GET | `/equipment/mine` | List equipment associated with the current user |
| GET | `/equipment/{equipment_id}` | Retrieve equipment details |
| PATCH | `/equipment/{equipment_id}` | Update equipment |
| POST | `/equipment/{equipment_id}/approve` | Approve equipment |
| POST | `/equipment/{equipment_id}/return` | Return equipment for correction |
| POST | `/equipment/{equipment_id}/resubmit` | Resubmit equipment |
| POST | `/equipment/{equipment_id}/documents` | Upload an equipment document |
| GET | `/equipment/documents/{doc_id}/download` | Download an equipment document |
| DELETE | `/equipment/documents/{doc_id}` | Delete an equipment document |
| POST | `/equipment/import-csv` | Import equipment from CSV |

## 6. Fault Management Endpoints

Base path: `/faults`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/` | Create a fault report |
| GET | `/faults/` | List fault reports |
| GET | `/faults/{fault_id}` | Retrieve a fault report |
| POST | `/faults/{fault_id}/assign` | Assign a fault |
| POST | `/faults/{fault_id}/status` | Update fault status |
| POST | `/faults/{fault_id}/close` | Close a fault report |
| GET | `/faults/priority-list` | Retrieve the fault priority list |

## 7. Fault Assessment Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/{fault_id}/assessments` | Create a fault assessment |
| GET | `/faults/{fault_id}/assessments` | Retrieve fault assessments |

## 8. Repair Work Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/{fault_id}/repairs` | Record repair work |
| POST | `/faults/{fault_id}/tests` | Record repair testing |
| POST | `/faults/{fault_id}/release` | Record equipment release |
| GET | `/faults/{fault_id}/records` | Retrieve repair records |

## 9. Repair Verification Endpoints

Base path: `/repair-verification-records`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/repair-verification-records/` | Create a verification record |
| GET | `/repair-verification-records/` | List verification records |
| GET | `/repair-verification-records/{record_id}` | Retrieve a verification record |
| PUT | `/repair-verification-records/{record_id}` | Update a verification record |
| DELETE | `/repair-verification-records/{record_id}` | Delete a verification record |

**Important:** These endpoints require a `user_id` HTTP header.

The list endpoint supports pagination through `skip` and `limit` parameters.

## 10. Maintenance Reporting Endpoints

Base path: `/reports`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/reports/maintenance-summary` | Retrieve a maintenance summary |
| GET | `/reports/maintenance-summary/pdf` | Generate a maintenance summary PDF |

## 11. Health Check Endpoint

| Method | Endpoint | Description |
|---|---|---|
| GET | `/health` | Check backend application availability |

The health endpoint returns:

```json
{
  "status": "ok"
}

```

## 12. API Error Handling

The backend uses a centralized service error handler.

Service errors are returned with:

- An HTTP status code configured by the service error.
- A JSON response containing a `detail` field.

The frontend API client also provides an `ApiError` class for handling HTTP errors.

## 13. API Documentation Notes

- Endpoint paths reflect routes registered by the FastAPI application.
- HTTP methods identify the supported operation.
- Request bodies and response schemas should be checked against the corresponding endpoint implementation.
- Authentication and authorization requirements should be verified for each endpoint.
- Repair verification endpoints require a `user_id` HTTP header.

## 14. Related Documentation

- [Backend Documentation](backend-documentation.md)
- [Authentication and Security](authentication-and-security.md)
- [Database Design](database-design.md)
- [System Architecture](architecture.md)
- [Technical Reference](technical-reference.md)

## Interactive API Explorer

Waliin provides interactive API documentation through Swagger UI. The documentation allows developers to explore the backend API endpoints, inspect request parameters, review response schemas and understand available operations.

**Backend API Documentation:**

[Open Waliin Swagger UI](https://waliin-8c96dd4bd190.herokuapp.com/docs)