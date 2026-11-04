
# Waliin Project Overview

## 1. Introduction

Waliin is a healthcare equipment management system developed by Solvya. It is designed to support the management and monitoring of medical equipment within healthcare facilities.

The platform brings equipment information and maintenance-related activities into one system, helping users manage equipment records, report faults, coordinate repair activities, and monitor equipment maintenance.

### 1.1 Documentation Scope

This documentation describes Waliin's system structure, technical implementation, functionality, and development workflows.

It draws on the project documentation, frontend and backend application repositories, and testing activities conducted during development.

Individual implementation details and operational behaviour should be interpreted in the context of the relevant application code and verification results.

## 2. Project Purpose

Waliin provides a structured way to manage the lifecycle of healthcare equipment.

Its main objectives are to:

- Maintain records of medical equipment.
- Support equipment registration and documentation.
- Allow users to report equipment faults.
- Support technical assessment and repair tracking.
- Record repair verification activities.
- Coordinate resource requests and external support.
- Provide maintenance summaries and reports.
- Support communication through system notifications.

## 3. Intended Users

Waliin defines three main user roles:

| User role | General responsibility |
|---|---|
| `health_manager` | Health management and administrative activities |
| `biomedical_engineer` | Equipment assessment, maintenance, and technical activities |
| `clinical_staff` | Clinical equipment-related activities and fault reporting |

## 4. Core System Capabilities

### 4.1 Equipment Management

Waliin supports the registration and management of medical equipment records. Equipment information can be maintained and updated through the application.

The backend provides operations for:

- Creating equipment records.
- Listing and retrieving equipment.
- Updating equipment information.
- Reviewing pending equipment records.
- Approving or returning equipment records.
- Importing equipment records through CSV.
- Managing equipment-related documents.

### 4.2 Fault Management

Users can report equipment faults. The system provides functionality for retrieving fault records, assigning faults, updating their status, and closing faults.

### 4.3 Technical Assessment and Repair

The backend supports fault assessments, technical findings, repair records, testing, and equipment release operations.

### 4.4 Repair Verification

Waliin provides repair verification records to document repair activities, test results, and equipment release decisions.

### 4.5 Resource Requests and Follow-ups

The system supports requests for spare parts, technical support, replacement resources, and new equipment.

It also provides functionality for recording follow-up communications and responses relating to resource requests.

### 4.6 Notifications

Waliin provides in-app notifications to communicate relevant equipment, fault, and resource-request updates to users.

### 4.7 Maintenance Reporting

The system provides maintenance summary data and a PDF maintenance summary endpoint.

## 5. Technology Overview

The main technologies used by Waliin include:

| Layer | Technology |
|---|---|
| Frontend framework | Next.js |
| User interface | React |
| Frontend language | TypeScript |
| Backend framework | FastAPI |
| Backend language | Python |
| Database | PostgreSQL |
| Database integration | SQLAlchemy |
| Database migrations | Alembic |

## 6. Related Documentation

Use the following pages for more detailed technical information:

- [System Architecture](architecture.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [API Reference](api-reference.md)
- [Database Design](database-design.md)
- [Authentication and Security](authentication-and-security.md)
- [Deployment Guide](deployment-guide.md)
- [Developer Guide](developer-guide.md)
- [Testing](testing.md)
- [Technical Reference](technical-reference.md)
