
# Testing

## 1. Introduction

Testing helps verify that Waliin behaves as expected and that changes do not introduce unintended problems.

Waliin has separate frontend and backend projects, each with its own testing and quality-check tools.

## Documentation and evidence boundary

This repository contains the technical documentation site rather than the underlying application implementation or test suite. The testing guidance in this section reflects recommended verification practices for the documented system, but it is not evidence of executed application tests in this repository.

The validation steps described here should be treated as project guidance unless they are confirmed against the authoritative application repository and runtime environment.

This guide describes the available testing tools, functional testing areas and recommended verification workflow.

## 2. Frontend Testing

The frontend uses Vitest as its test runner.

The `package.json` file defines the following test command:

```bash
npm run test
```

This runs:

```bash
vitest run --passWithNoTests
```

The frontend also provides additional quality-check commands:

| Command | Purpose |
|---|---|
| `npm run test` | Run frontend tests |
| `npm run lint` | Run ESLint |
| `npm run format:check` | Check code formatting |
| `npm run format` | Format project files |
| `npm run build` | Build the Next.js application |

The frontend test suite supports verification of individual application components and functionality.

The `--passWithNoTests` option allows the test command to complete successfully when no test files are present.

## 3. Backend Testing

The backend uses pytest for automated testing.

Ruff is used for Python code-quality checks.

### 3.1 Running Backend Tests

From the backend project directory, run:

```bash
uv run pytest -q
```

To run tests for a specific module or test directory:

```bash
uv run pytest tests/
```

### 3.2 Code Quality Checks

Run Ruff to check Python code quality:

```bash
uv run ruff check .
```

These tools support verification of backend functionality, expected application behaviour and code consistency.

## 4. Testing Scope

Testing activities should cover the main functional areas of Waliin.

### 4.1 Authentication

Verify:

- User login and logout.
- Current-user retrieval.
- Invitation acceptance.
- Password reset operations.
- Multi-factor authentication operations.
- Session handling and authentication requirements.

### 4.2 Equipment Management

Verify:

- Equipment registration.
- Equipment retrieval and updates.
- Equipment approval and return operations.
- Equipment document handling.
- CSV equipment import.

### 4.3 Fault and Repair Management

Verify:

- Fault creation and retrieval.
- Fault assignment and status updates.
- Fault assessments.
- Repair records and tests.
- Equipment release operations.
- Repair verification records.

### 4.4 Maintenance Reporting

Verify:

- Maintenance summary retrieval.
- Maintenance summary PDF generation.

### 4.5 Notifications and Resource Requests

Verify:

- Notification retrieval and relevant status updates.
- Resource request creation and retrieval.
- Request item management.
- Request follow-up operations.

## 5. API Verification

Backend API endpoints should be checked for:

- Expected HTTP status codes.
- Valid request and response data.
- Appropriate error responses.
- Authentication requirements.
- Role-based access restrictions.
- Correct database interactions.
- Appropriate handling of invalid or missing data.

API verification can be performed through automated backend tests and the interactive Swagger UI.

[Open Waliin Swagger UI](https://waliin-8c96dd4bd190.herokuapp.com/docs)

## 6. Frontend Verification

Frontend verification should cover:

- Page rendering and navigation.
- Form validation.
- User authentication flows.
- API request and response handling.
- Loading and error states.
- Role-oriented navigation.
- Equipment registration and management workflows.
- Fault reporting and repair-related workflows.

Frontend verification should confirm that user actions produce the expected interface responses and that backend errors are communicated appropriately.

## 7. Testing Workflow

A typical verification workflow is:

1. Identify the functionality being changed.
2. Review the relevant frontend and backend code.
3. Run the relevant automated tests.
4. Run linting and formatting checks.
5. Build the frontend when frontend code changes.
6. Verify the affected application functionality.
7. Document any known issues.

### 7.1 Recommended Verification Commands

Backend:

```bash
uv run pytest -q
uv run ruff check .
```

Frontend:

```bash
npm run test
npm run lint
npm run format:check
npm run build
```

Run the relevant checks from the respective project directories.

## 8. Test Reporting

Testing results should record:

- The tests or checks performed.
- The result of each test run.
- Any failures or warnings.
- Known issues that remain unresolved.
- Relevant changes made to address identified problems.

Test results should reflect actual execution. A successful build or lint check should not be reported as evidence that all application workflows have been tested.

## 9. Related Documentation

- [Developer Guide](developer-guide.md)
- [Deployment Guide](deployment-guide.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [API Reference](api-reference.md)
- [Database Design](database-design.md)
- [Authentication and Security](authentication-and-security.md)
