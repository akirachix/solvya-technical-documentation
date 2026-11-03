
# API Reference

## 1. Introduction

This document describes the HTTP API endpoints registered by the Waliin FastAPI backend.

The API supports authentication, user management, dashboard information, equipment management, fault reporting, technical assessments, repair verification, maintenance reporting, notifications, and resource requests.

The backend is built using FastAPI and exposes RESTful endpoints that allow the frontend applications to communicate with the system.

## 2. API Information

| Property | Value |
|---|---|
| Application | Waliin API |
| Framework | FastAPI |
| API version | 0.1.0 |
| Data format | JSON |
| Database | PostgreSQL |
| Health endpoint | `/health` |
| Interactive documentation | `/docs` |
| OpenAPI schema | `/openapi.json` |

The backend routers are registered in `main.py`.

The frontend can use `BACKEND_API_PREFIX` to configure the API prefix. The endpoint paths documented below represent the routes declared by the FastAPI routers.

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
| POST | `/users` | Create a user invitation |
| GET | `/users` | Retrieve users |
| PATCH | `/users/{user_id}` | Update a user |
| POST | `/users/{user_id}/resend-invite` | Resend a user invitation |
| POST | `/users/{user_id}/revoke` | Revoke a user |
| POST | `/users/{user_id}/send-reset-link` | Send a password reset link |

User management operations are restricted to health managers.

## 5. Dashboard Endpoints

Base path: `/dashboard`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/dashboard/summary` | Retrieve dashboard summary information |

The dashboard endpoint provides summary information used by the management dashboard.

## 6. Equipment Management Endpoints

Base path: `/equipment`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/equipment/departments` | Create a department |
| GET | `/equipment/departments` | List departments |
| GET | `/equipment/departments/{department_id}` | Retrieve a department |
| PATCH | `/equipment/departments/{department_id}` | Update a department |
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

## 7. Fault Management Endpoints

Base path: `/faults`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/` | Create a fault report |
| GET | `/faults/` | List fault reports |
| GET | `/faults/{fault_id}` | Retrieve a fault report |
| POST | `/faults/{fault_id}/assign` | Assign a fault to a biomedical engineer |
| POST | `/faults/{fault_id}/status` | Update fault status |
| POST | `/faults/{fault_id}/close` | Close a fault report |

## 8. Fault Assessment Endpoints

Base path: `/faults`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/{fault_id}/assessments` | Create a fault assessment |
| GET | `/faults/{fault_id}/assessments` | Retrieve fault assessments |

These endpoints support technical assessment and rule-based fault prioritisation.

## 9. Priority List Endpoints

Base path: `/faults`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/faults/priority-list` | Retrieve the prioritised fault list |

The priority list provides information used to support equipment maintenance and repair prioritisation.

## 10. Repair Work Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/faults/{fault_id}/repairs` | Record repair work |
| POST | `/faults/{fault_id}/tests` | Record repair testing |
| POST | `/faults/{fault_id}/release` | Record equipment release |
| GET | `/faults/{fault_id}/records` | Retrieve repair records |

These endpoints support the documentation of repair activities, functional testing, safety testing, and equipment release.

## 11. Repair Verification Endpoints

Base path: `/repair-verification-records`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/repair-verification-records/` | Create a verification record |
| GET | `/repair-verification-records/` | List verification records |
| GET | `/repair-verification-records/{record_id}` | Retrieve a verification record |
| PUT | `/repair-verification-records/{record_id}` | Update a verification record |
| DELETE | `/repair-verification-records/{record_id}` | Delete a verification record |

The list endpoint supports pagination through `skip` and `limit` query parameters.

## 12. Maintenance Reporting Endpoints

Base path: `/reports`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/reports/maintenance-summary` | Retrieve a maintenance summary |
| GET | `/reports/maintenance-summary/pdf` | Generate and download a maintenance summary PDF |

These endpoints provide maintenance information for reporting and management purposes.

## 13. Notification Endpoints

Base path: `/notifications`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/notifications/` | Create a notification |
| GET | `/notifications/` | List notifications |
| GET | `/notifications/me` | Retrieve notifications for the current user |
| GET | `/notifications/{id}` | Retrieve a specific notification |
| POST | `/notifications/{id}/read` | Mark a notification as read |

The notification endpoints support in-app notifications and read-status tracking.

## 14. Resource Request Endpoints

These endpoints manage requests for spare parts, technical support, replacement resources, and new equipment.

| Method | Endpoint | Description |
|---|---|---|
| POST | `/requests` | Create a resource request |
| GET | `/requests` | List resource requests |
| GET | `/requests/overdue` | Retrieve overdue resource requests |
| GET | `/requests/{request_id}` | Retrieve a specific resource request |
| PATCH | `/requests/{request_id}` | Update a resource request |
| POST | `/requests/{request_id}/decide` | Approve or reject a resource request |

## 15. Request Item Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/requests/{request_id}/items` | Retrieve items associated with a resource request |
| PATCH | `/requests/{request_id}/items/{item_id}` | Update a requested item |

These endpoints manage individual items and their quantities within resource requests.

## 16. Request Follow-up Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/requests/{request_id}/follow-ups` | Create a follow-up record |
| GET | `/requests/{request_id}/follow-ups` | Retrieve follow-ups for a resource request |
| POST | `/follow-ups/{follow_up_id}/reply` | Record a response to a follow-up |
| PATCH | `/follow-ups/{follow_up_id}` | Update a follow-up record |

Follow-up records document external communication and responses relating to resource requests.

## 17. Health Check Endpoint

| Method | Endpoint | Description |
|---|---|---|
| GET | `/health` | Check backend application availability |

The health endpoint returns a JSON response indicating application availability.

Example response:

```json
{
  "status": "ok"
}
```

## 18. API Error Handling

The backend uses a centralized service error handler.

Service errors are returned with:

- An HTTP status code configured by the service error.
- A JSON response containing a `detail` field.

The frontend API client also provides an `ApiError` class for handling HTTP errors.

## 19. API Documentation Notes

- Endpoint paths reflect routes registered by the FastAPI application.
- HTTP methods identify the supported operation.
- Request bodies and response schemas should be checked against the corresponding endpoint implementation.
- Authentication and authorization requirements should be verified for each endpoint.
- Some endpoints use the authenticated session cookie, while others have their own request-level identity or role handling.
- Pagination parameters are available on supported list endpoints.
- The interactive Swagger documentation provides additional information about request parameters, response schemas, and endpoint operations.

## 20. Related Documentation

- [Backend Documentation](backend-documentation.md)
- [Authentication and Security](authentication-and-security.md)
- [Database Design](database-design.md)
- [System Architecture](architecture.md)
- [Technical Reference](technical-reference.md)

## 21. Interactive API Explorer

Waliin provides interactive API documentation through Swagger UI.

The documentation allows developers to:

- Explore registered backend API endpoints.
- Inspect request parameters and request bodies.
- Review response schemas.
- Understand available HTTP operations.
- Test API operations through the interactive interface.

**Backend API Documentation:**

[Open Waliin Swagger UI](https://waliin-8c96dd4bd190.herokuapp.com/docs)
