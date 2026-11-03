# Authentication and Security

## 1. Introduction

Waliin uses a backend authentication system to control access to application functionality and protect user accounts.

Authentication is implemented through the FastAPI backend. The frontend communicates with the authentication endpoints through its API client.

## 2. User Roles

The backend defines three user roles:

| Role | Description |
|---|---|
| `health_manager` | Health management user |
| `biomedical_engineer` | Biomedical engineering user |
| `clinical_staff` | Clinical staff user |

These roles identify the categories of users supported by the application.

## 3. Authentication Features

The backend provides the following authentication operations:

- User login and logout.
- Retrieving the currently authenticated user.
- Multi-factor authentication setup.
- Multi-factor authentication confirmation.
- Multi-factor authentication verification.
- Invitation acceptance.
- Password reset requests.
- Password reset completion.

## 4. Authentication API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/auth/login` | Authenticate a user |
| POST | `/auth/logout` | End the authenticated session |
| GET | `/auth/me` | Retrieve the current user |
| POST | `/auth/mfa/setup` | Begin MFA setup |
| POST | `/auth/mfa/confirm` | Confirm MFA setup |
| POST | `/auth/mfa/verify` | Verify MFA |
| POST | `/auth/accept-invite` | Accept a user invitation |
| POST | `/auth/forgot-password` | Request a password reset |
| POST | `/auth/reset-password` | Complete a password reset |

## 5. Session Management

The backend uses a session cookie named:

`__Host-waliin_session`

The cookie is configured with the following security attributes:

| Attribute | Configuration |
|---|---|
| Secure | Enabled |
| HttpOnly | Enabled |
| SameSite | Strict |
| Path | `/` |
| Idle timeout | 15 minutes |
| Maximum session lifetime | 8 hours |

These settings help protect session cookies and limit how long sessions remain valid.

## 6. Password Security

The backend uses Argon2 password hashing through the `pwdlib` library.

Password hashing protects stored password credentials by avoiding storage of passwords as plain text.

## 7. Multi-Factor Authentication

Waliin includes backend endpoints for:

- Starting MFA setup.
- Confirming MFA setup.
- Verifying MFA during authentication.

These operations are handled by the authentication API.

## 8. Authorization and User Access

Waliin defines role categories for health managers, biomedical engineers and clinical staff.

The frontend also uses role information to determine the navigation and user experience presented after login.

The existence of a role does not, by itself, establish the exact permissions available to that role. Those permissions should be verified against the backend authorization implementation.

## 9. Related Documentation

- [Backend Documentation](backend-documentation.md)
- [API Reference](api-reference.md)
- [System Architecture](architecture.md)

## Security Architecture Resource

The following Software System Architecture Document (SSAD) is provided as an additional reference for the system's security architecture.

### Software System Architecture Document (SSAD)

[Open Waliin SSAD – Figma](https://www.figma.com/board/tYkPMimzCkAXrX8OZTOQpa/Solvya-SSAD?node-id=0-1&p=f)

