# Testing

## 1. Introduction

Testing helps verify that Waliin behaves as expected and that changes do not introduce unintended problems.

Waliin has separate frontend and backend projects, each with its own testing and quality-check tools.

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
| `npm run lint` | Run ESLint |
| `npm run format:check` | Check code formatting |
| `npm run format` | Format project files |
| `npm run build` | Build the Next.js application |

## 3. Backend Testing

The backend uses pytest for automated testing.

Ruff is used for Python code-quality checks.

These tools support the verification of backend functionality and code consistency.

## 4. Testing Scope

Testing activities should cover the main functional areas of Waliin.

### 4.1 Authentication

Verify:

- User login and logout.
- Current-user retrieval.
- Invitation acceptance.
- Password reset operations.
- Multi-factor authentication operations.

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

## 5. API Verification

Backend API endpoints should be checked for:

- Expected HTTP status codes.
- Valid request and response data.
- Appropriate error responses.
- Authentication requirements.
- Correct database interactions.

## 6. Frontend Verification

Frontend verification should cover:

- Page rendering and navigation.
- Form validation.
- User authentication flows.
- API request and response handling.
- Loading and error states.
- Role-oriented navigation.

## 7. Testing Workflow

A typical verification workflow is:

1. Identify the functionality being changed.
2. Review the relevant frontend and backend code.
3. Run the relevant automated tests.
4. Run linting and formatting checks.
5. Build the frontend when frontend code changes.
6. Verify the affected application functionality.
7. Document any known issues.

## 8. Related Documentation

- [Developer Guide](developer-guide.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [API Reference](api-reference.md)
- [Database Design](database-design.md)