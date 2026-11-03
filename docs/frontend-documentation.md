# Frontend Documentation

## 1. Introduction

Waliin's frontend is a web application developed using Next.js, React and TypeScript.

It provides the user interface through which users interact with healthcare equipment management functionality.

The application uses the Next.js App Router and communicates with the FastAPI backend through HTTP API requests.

## 2. Technology Stack

| Technology | Version | Purpose |
|---|---|---|
| Next.js | 16.4.3 | Frontend framework |
| React | 19.3.0 | User interface library |
| TypeScript | 5.x | Frontend programming language |
| Tailwind CSS | 4.x | Styling framework |
| React Hook Form | 7.x | Form management |
| Lucide React | 1.x | Interface icons |
| Vitest | 5.x | Testing framework |
| ESLint | 9.x | Code quality checks |

## 3. Frontend Project Structure

The frontend project organizes its implementation into application routes, reusable components and shared utilities.

### 3.1 Main directories

| Directory | Responsibility |
|---|---|
| `app/` | Application routes and page components |
| `app/shared-paths/` | Shared header and sidebar components |
| `components/` | Reusable interface components |
| `lib/` | API client, authentication and application utilities |
| `public/` | Static application assets |

### 3.2 Application entry points

The root layout is defined in `app/layout.tsx`.

It configures:

- Application-wide layout.
- Inter font.
- Page metadata.
- Document language.
- Browser theme colour.
- Global styles.

The application uses `globals.css` for global styling and Tailwind CSS utilities.

## 4. Authentication Integration

The frontend uses shared authentication utilities defined in `lib/auth.ts`.

The authentication functionality includes:

- User login.
- Current-user retrieval.
- Logout.
- Password reset requests.
- Password reset completion.
- Invitation acceptance.
- Multi-factor authentication setup and verification.

### 4.1 User roles

The frontend recognizes three user roles:

| Role | Description |
|---|---|
| `health_manager` | Health management user |
| `biomedical_engineer` | Biomedical engineering user |
| `clinical_staff` | Clinical staff user |

### 4.2 Authentication state

The `UserProfileProvider` provides user profile information through React context.

It retrieves the current user through the backend authentication API and exposes the user information to application components.

## 5. API Integration

The shared API client is implemented in:

`lib/api/client.ts`

The main function is `apiFetch<T>()`.

Its responsibilities include:

- Sending requests to the frontend `/api` route.
- Including browser credentials.
- Setting JSON request headers.
- Parsing JSON responses.
- Handling HTTP errors.
- Returning `undefined` for HTTP 204 responses.

### 5.1 API errors

The frontend defines an `ApiError` class that extends JavaScript's `Error` class.

It includes an HTTP status code to help application components handle failed API requests.

### 5.2 Backend connectivity

The Next.js configuration supports:

- `BACKEND_URL`
- `BACKEND_API_PREFIX`

When `BACKEND_URL` is configured, the application can rewrite frontend `/api` requests to the configured backend API.

## 6. Application Routes

The frontend uses the Next.js App Router.

The following application routes are present in the project:

| Route | Purpose |
|---|---|
| `/login` | User login |
| `/forgot-password` | Password reset request |
| `/reset-password/[token]` | Password reset |
| `/accept-invite` | Invitation acceptance |
| `/get-started` | Getting started |
| `/onboarding` | User onboarding |
| `/continue-as` | Continue-as flow |
| `/biomedical-engineer/dashboard` | Biomedical engineer dashboard |
| `/biomedical-engineer/equipment` | Equipment management |
| `/biomedical-engineer/equipment/list` | Equipment listing |
| `/biomedical-engineer/register-equipment` | Equipment registration |
| `/biomedical-engineer/faults` | Fault management |
| `/biomedical-engineer/faults/[faultId]` | Fault details |

## 7. Shared Interface Components

The frontend includes shared interface components for consistent navigation and user information.

### 7.1 Header

The shared header provides:

- Search input.
- Notifications control.
- User profile information.
- User initials and role information.

### 7.2 Sidebar

The biomedical engineer sidebar provides navigation links for:

- Dashboard.
- Equipment.
- Maintenance.
- Requests.
- Reports.
- Settings.

The sidebar uses the current route to determine the active navigation item.

## 8. Equipment Management Interface

The biomedical engineer interface includes equipment registration and management functionality.

Equipment registration components include:

- `EquipmentDetails`
- `LocationSpecs`
- `PhotoDocs`
- `RegistrationMethod`
- `ReviewDetails`
- `SuccessState`
- `CsvEquipmentImport`

These components support the equipment registration workflow and CSV import interface.

## 9. Frontend Styling

The frontend uses Tailwind CSS 4 and global styles defined in `app/globals.css`.

The global styling defines:

- Inter typography.
- Application background and foreground colours.
- Brand colour variables.
- Shared visual styling.

## 10. Testing and Build Commands

The frontend provides these npm scripts:

| Command | Purpose |
|---|---|
| `npm run dev` | Start development server |
| `npm run build` | Build production application |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run test` | Run Vitest |
| `npm run format:check` | Check code formatting |
| `npm run format` | Format project files |

## 11. Related Documentation

- [System Architecture](architecture.md)
- [API Reference](api-reference.md)
- [Backend Documentation](backend-documentation.md)
- [Database Design](database-design.md)
- [Authentication and Security](authentication-and-security.md)
- [Developer Guide](developer-guide.md)

## Frontend Application Resources

The following links provide access to the deployed Waliin frontend applications.

### Progressive Web Application (PWA)

The Waliin PWA provides users with access to key equipment management functions, including fault reporting and equipment requests.

[Open Waliin PWA](https://waliin-solvya.vercel.app/home)

### Waliin Dashboard

The Waliin Dashboard provides the main interface for accessing the system's management functionality.

[Open Waliin Dashboard](https://waliin.vercel.app/)

### Solvya Informational Website

The informational website introduces Solvya and provides an overview of its work and solutions.

[Visit Solvya Website](https://solvya-website-lilac.vercel.app/)