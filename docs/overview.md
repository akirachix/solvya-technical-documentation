# Waliin Project Overview

## 1. Introduction

Waliin is a healthcare equipment management system developed by Solvya. It is designed to support the management and monitoring of medical equipment within healthcare facilities.

The platform brings equipment information and maintenance-related activities into one system, helping users manage equipment records, report faults and follow repair activities.

## 2. Project Purpose

Waliin provides a structured way to manage the lifecycle of healthcare equipment.

Its main objectives are to:

- Maintain records of medical equipment.
- Support equipment registration and documentation.
- Allow users to report equipment faults.
- Support technical assessment and repair tracking.
- Record repair verification activities.
- Provide maintenance summaries and reports.

## 3. Intended Users

Waliin defines three main user roles:

| User role | General responsibility |
|---|---|
| `health_manager` | Health management activities |
| `biomedical_engineer` | Equipment assessment and technical activities |
| `clinical_staff` | Clinical equipment-related activities |

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

### 4.2 Fault Management

Users can report equipment faults. The system provides functionality for retrieving fault records, assigning faults, updating their status and closing faults.

### 4.3 Technical Assessment and Repair

The backend supports fault assessments, repair records, testing and equipment release operations.

### 4.4 Repair Verification

Waliin provides repair verification records to document verification activities associated with equipment repairs.

### 4.5 Maintenance Reporting

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
- [API Reference](api-reference.md)
- [Database Design](database-design.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)

