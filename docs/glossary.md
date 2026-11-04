
# Glossary

## 1. Introduction

This glossary explains the technical terms, application concepts and abbreviations used throughout the Waliin technical documentation.

It provides a common reference for developers, technical reviewers and other stakeholders working with or reviewing the system.

## 2. Application and Technology Terms

| Term | Definition |
|---|---|
| Waliin | Healthcare equipment management system developed by Solvya to support medical equipment management in healthcare facilities. |
| Solvya | Company responsible for developing Waliin. |
| Frontend | User-facing part of the application through which users interact with the system. |
| Backend | Server-side application responsible for processing requests, enforcing application logic and managing data operations. |
| API | Application Programming Interface that enables communication between software components. |
| REST API | API architectural style that uses HTTP methods to access and manage resources. |
| Next.js | React framework used to build the Waliin frontend. |
| React | JavaScript library used to build user interfaces. |
| TypeScript | Programming language used to develop the frontend with static type checking. |
| FastAPI | Python framework used to implement the Waliin backend API. |
| PostgreSQL | Relational database management system used to store application data. |
| SQLAlchemy | Python library used for database interaction and object-relational mapping. |
| Alembic | Database migration tool used to manage changes to the database schema. |
| Pydantic | Python library used for data validation and settings management. |
| Vitest | Test runner used by the frontend project. |
| pytest | Testing framework used by the backend project. |
| Progressive Web Application (PWA) | Web application designed to provide an app-like experience through supported browsers and devices. |
| Role-Based Access Control (RBAC) | Access control approach in which permissions are assigned according to user roles. |

## 3. Healthcare and Equipment Management Terms

| Term | Definition |
|---|---|
| Medical Equipment | Equipment used to support healthcare services and clinical activities. |
| Equipment Registration | Process of creating an equipment record in Waliin. |
| Equipment Record | Stored information describing a registered piece of medical equipment. |
| Equipment Approval | Administrative process of reviewing and approving an equipment record before it becomes an accepted system record. |
| Equipment Document | File associated with an equipment record, such as a user manual, warranty document or service document. |
| Equipment Status | Recorded operational or administrative state of a piece of equipment. |
| Installation Status | Recorded state of equipment installation and commissioning. |
| Equipment Fault | Reported problem affecting the operation or functionality of medical equipment. |
| Fault Reporting | Process through which clinical staff submit an equipment fault using the application. |
| Fault Assessment | Technical evaluation of a reported equipment fault by a biomedical engineer. |
| Biomedical Engineer | User role responsible for equipment inspection, fault assessment, maintenance and repair activities. |
| Clinical Staff | User role responsible for reporting equipment-related issues and providing relevant clinical context. |
| Health Manager | User role responsible for management activities, including user administration, equipment oversight and maintenance reporting. |
| Repair Record | Record documenting repair activities performed on equipment. |
| Repair Verification | Process of recording checks performed to establish whether repaired equipment can return to service. |
| Maintenance | Activities performed to assess, maintain or restore medical equipment. |
| Maintenance Report | Report containing information about equipment maintenance activities and their outcomes. |
| Equipment Downtime | Period during which equipment is unavailable for its intended operational use. |
| Equipment Prioritisation | Process of assigning priority to equipment or reported faults according to defined criteria. |
| Rule-Based Prioritisation | Approach that uses predefined rules and criteria to determine equipment or fault priority. |
| External Support Request | Request for assistance from an external organisation or service provider when support is required beyond available hospital resources. |
| Support Information | Information about available equipment support, such as warranties, service contracts, supplier details or donor commitments. |
| CSV Import | Process of importing equipment records from a Comma-Separated Values file. |

## 4. Authentication and Security Terms

| Term | Definition |
|---|---|
| Authentication | Process of verifying a user's identity before granting access to the application. |
| Authorization | Process of determining which resources and operations an authenticated user is permitted to access. |
| Session | Period during which a user remains authenticated with the application. |
| Session Cookie | Browser cookie used to maintain an authenticated session. |
| Multi-Factor Authentication (MFA) | Authentication process requiring additional verification beyond a user's primary authentication factor. |
| Password Hashing | Process of transforming a password into a one-way cryptographic representation for secure storage. |
| Argon2 | Password-hashing algorithm designed to protect stored passwords against password-guessing attacks. |
| Role-Based Access | Approach to managing application permissions according to assigned user roles. |
| Access Control | Mechanisms used to restrict access to application resources and operations. |

## 5. Database and API Terms

| Term | Definition |
|---|---|
| Database | Organised collection of data managed by a database management system. |
| Relational Database | Database that stores information in related tables. |
| Database Table | Structure that stores records in rows and columns. |
| Primary Key | Column or combination of columns that uniquely identifies a database record. |
| Foreign Key | Column or combination of columns that references a record in another database table. |
| Database Migration | Versioned change to the database schema used to update its structure. |
| Index | Database structure that helps improve data retrieval performance. |
| Database View | Virtual table based on the result of a database query. |
| Object-Relational Mapping (ORM) | Technique that maps application objects to relational database tables. |
| HTTP | Protocol used for communication between clients and servers. |
| GET | HTTP method used to retrieve resources. |
| POST | HTTP method commonly used to submit data or create resources. |
| PATCH | HTTP method used to partially update a resource. |
| PUT | HTTP method commonly used to replace a resource or update its representation. |
| DELETE | HTTP method used to request removal of a resource. |
| JSON | Data format used for structured API communication. |
| HTTP Status Code | Numeric response code indicating the outcome of an HTTP request. |
| Endpoint | Specific API URL through which an operation can be accessed. |
| Request | Message sent by a client to an API. |
| Response | Message returned by an API after processing a request. |
| Request Validation | Process of checking incoming request data against defined requirements before processing it. |
| API Documentation | Reference describing available API endpoints, request formats, response formats and expected behaviour. |

## 6. Abbreviations

| Abbreviation | Meaning |
|---|---|
| API | Application Programming Interface |
| CSV | Comma-Separated Values |
| DB | Database |
| HTTP | Hypertext Transfer Protocol |
| HTTPS | Hypertext Transfer Protocol Secure |
| MFA | Multi-Factor Authentication |
| ORM | Object-Relational Mapping |
| PDF | Portable Document Format |
| PWA | Progressive Web Application |
| REST | Representational State Transfer |
| RBAC | Role-Based Access Control |
| SQL | Structured Query Language |
| UI | User Interface |
| URL | Uniform Resource Locator |
| JSON | JavaScript Object Notation |

## 7. Related Documentation

For more information about the concepts covered in this glossary, refer to:

- [Project Overview](overview.md)
- [System Architecture](architecture.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [API Reference](api-reference.md)
- [Database Design](database-design.md)
- [Authentication and Security](authentication-and-security.md)
- [Testing](testing.md)
