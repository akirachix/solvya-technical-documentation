# Database Design

## 1. Overview

Waliin uses a relational database to manage healthcare equipment, users, departments, faults, repair activities, resource requests, notifications, and audit records.

The database schema is managed using **SQLAlchemy ORM models** and **Alembic migrations**. The initial migration, `0001_create_all_tables.py`, creates 13 physical tables, a PostgreSQL enum type, database functions and triggers, and the `fault_downtime` view.

The database uses PostgreSQL-specific features, including UUID generation, JSONB columns, partial unique indexes, triggers, and a native enum type.

## 2. Database Schema

The initial migration creates the following 13 tables.

| Table | Purpose |
|---|---|
| `users` | Stores user accounts, roles, department assignments, invitation information, password-reset information, and MFA settings. |
| `departments` | Stores hospital departments and their assigned responsible biomedical engineers. |
| `equipment` | Stores medical equipment registration details, ownership information, approval status, installation status, and service status. |
| `equipment_documents` | Stores metadata and storage references for equipment-related documents. |
| `faults` | Records reported equipment faults, their severity, status, and assigned biomedical engineers. |
| `fault_assessments` | Stores technical assessments and calculated fault-priority information. |
| `fault_status_history` | Records changes to fault statuses. |
| `repair_verification_records` | Stores repair activities, test results, and authorization to return equipment to service. |
| `resource_requests` | Records requests for spare parts, technical support, replacement resources, and new equipment. |
| `request_items` | Stores individual items and quantities associated with resource requests. |
| `request_follow_ups` | Records external communication and responses relating to resource requests. |
| `notifications` | Stores notifications and their delivery and read-status information. |
| `audit_logs` | Records user actions and changes to important system entities. |

### 2.1 Users

The `users` table stores account information and access-control data.

Important fields include:

- `user_id`: UUID primary key.
- `full_name`: User's full name.
- `email`: Unique email address.
- `password_hash`: Hashed password, which may be null for an account that has not completed invitation acceptance.
- `role`: User role.
- `department_id`: Optional department reference.
- `is_active`: Indicates whether the account is active.
- `invited_by`: Optional reference to the user who issued the invitation.
- Invitation token hash, expiry, and acceptance timestamp.
- Password-reset token hash and expiry.
- MFA enabled status and encrypted MFA secret.
- `token_version`: Account token-version value.
- `created_at`: Account creation timestamp.

The table enforces unique email addresses and unique combinations of user ID and role. It also enforces consistency between invitation, password, MFA, and password-reset fields.

Users with roles other than `health_manager` must have a department assigned.

### 2.2 Departments

The `departments` table represents hospital departments.

Important fields include:

- `department_id`: UUID primary key.
- `department_name`: Required unique department name.
- `description`: Optional department description.
- `responsible_engineer_id`: Optional reference to a responsible engineer.
- `responsible_engineer_role`: Defaults to `biomedical_engineer`.
- `is_active`: Indicates whether the department is active.
- `created_at`: Creation timestamp.

The responsible engineer reference uses a composite foreign key to ensure that the assigned user has the `biomedical_engineer` role.

### 2.3 Equipment

The `equipment` table stores medical equipment registration and lifecycle information.

Important fields include:

- `equipment_id`: UUID primary key.
- `manufacturer`, `model_name`, and optional `model_number`.
- `equipment_category`.
- `department_id`: Department responsible for the equipment.
- `asset_tag`: Unique equipment identifier.
- Optional `serial_number`.
- `location`.
- `acquisition_type`.
- Optional donor or supplier information.
- Optional `received_at` date.
- `registration_status`.
- `installation_status`.
- `service_status`.
- Optional warranty start and end dates.
- `registered_by`: User who registered the equipment.
- Optional `approved_by` and `approved_at`.
- `approved_by_role`: Defaults to `health_manager`.
- Creation and update timestamps.

The table connects equipment to its department, registering user, approving user, documents, and reported faults.

### 2.4 Equipment Documents

The `equipment_documents` table stores document metadata and storage references.

Important fields include:

- `document_id`: UUID primary key.
- `equipment_id`: Associated equipment.
- `document_type`: Classification of the document.
- `document_name`: Document name.
- `storage_key`: Storage reference.
- Optional document and expiry dates.
- `uploaded_by`: User who uploaded the document.
- `uploaded_at`: Upload timestamp.

Document types include photos, manuals, warranties, donation letters, delivery notes, installation reports, and calibration certificates.

The table references both `equipment` and `users`.

### 2.5 Faults

The `faults` table records equipment faults.

Important fields include:

- `fault_id`: UUID primary key.
- `equipment_id`: Affected equipment.
- `reported_by`: User who reported the fault.
- `client_report_id`: Optional unique client-generated report identifier.
- `assigned_engineer_id`: Optional assigned biomedical engineer.
- `assigned_engineer_role`: Defaults to `biomedical_engineer`.
- `description`: Fault description.
- `severity`: Fault severity.
- `status`: Current fault status, defaulting to `reported`.
- `failure_observed_at`: Time the failure was observed.
- `reported_at`: Time the fault was reported.
- `out_of_service_at`: Time the equipment was taken out of service.
- `updated_at`: Last update timestamp.
- `closed_at`: Optional closure timestamp.

The table connects faults to equipment, reporting users, assigned engineers, status history, assessments, repair verification records, and resource requests.

### 2.6 Fault Assessments

The `fault_assessments` table stores technical assessments and fault-priority calculations.

Important fields include:

- `assessment_id`: UUID primary key.
- `fault_id`: Associated fault.
- `assessed_by`: Assessing user.
- `assessed_by_role`: Defaults to `biomedical_engineer`.
- `assessed_at`: Assessment timestamp.
- `findings`, `condition`, and `recommended_action`.
- `severity_factor`.
- `clinical_criticality`.
- `backup_available`.
- `history_factor`.
- `priority_score`.
- `rule_priority_level`.
- `priority_level`.
- `priority_explanation`.
- `rule_version`.
- `is_current`: Indicates whether the assessment is current.

A partial unique index named `uq_assessment_current` ensures that only one assessment per fault can be marked as current.

### 2.7 Fault Status History

The `fault_status_history` table maintains a record of fault-status changes.

Important fields include:

- `history_id`: UUID primary key.
- `fault_id`: Associated fault.
- `previous_status`: Previous status, which may be null.
- `new_status`: New status.
- `changed_by`: Optional user who changed the status.
- `reason`: Optional explanation.
- `changed_at`: Timestamp of the change.

A database constraint prevents the previous and new statuses from being identical.

### 2.8 Repair Verification Records

The `repair_verification_records` table records repair work, testing, and equipment release decisions.

Important fields include:

- `record_id`: UUID primary key.
- `fault_id` and `equipment_id`: Associated fault and equipment.
- `record_type`: Type of repair or verification record.
- `performed_by`: User who performed the work.
- `performed_by_role`: Defaults to `biomedical_engineer`.
- `work_performed`: Description of work.
- `parts_used`: Parts used during repair.
- `repair_started_at` and `repair_completed_at`.
- `test_result` and `test_details`.
- `authorized_for_service`: Indicates authorization to return equipment to service.
- `performed_at`: Record timestamp.
- `released_at`: Release timestamp.

The table uses a composite foreign key to ensure that the equipment associated with a record matches the equipment associated with its fault.

A partial unique index named `uq_record_one_release` allows only one authorized release record per fault.

### 2.9 Resource Requests

The `resource_requests` table stores requests made for resources needed to address equipment issues.

Important fields include:

- `request_id`: UUID primary key.
- `requested_by`: User who submitted the request.
- `related_fault_id`: Optional related fault.
- `request_type`: Type of resource request.
- `justification`: Reason for the request.
- `status`: Defaults to `pending`.
- `decision_by`: Optional decision-making user.
- `decision_by_role`: Defaults to `health_manager`.
- `decision_reason`: Optional decision explanation.
- `requested_at`, `decided_at`, and `resolved_at`.

A resource request can have multiple request items and follow-up records.

### 2.10 Request Items

The `request_items` table stores individual items belonging to a resource request.

Important fields include:

- `item_id`: UUID primary key.
- `request_id`: Associated resource request.
- `item_name`: Requested item.
- Optional `part_number`, `specification`, and `unit`.
- `quantity_requested`.
- Optional `quantity_approved`.
- `quantity_fulfilled`.

Database constraints ensure that requested quantities are positive, approved quantities do not exceed requested quantities, and fulfilled quantities do not exceed approved quantities when an approved quantity is recorded.

### 2.11 Request Follow-ups

The `request_follow_ups` table records follow-up communications associated with resource requests.

Important fields include:

- `follow_up_id`: UUID primary key.
- `request_id`: Associated request.
- `organisation`: External organisation contacted.
- `channel`: Communication channel.
- `sent_at`: Date the communication was sent.
- `next_follow_up_date`: Optional next follow-up date.
- `reply_status`: Defaults to `no_reply`.
- `reply_at`: Optional reply date.
- `note`: Optional communication note.
- `logged_by`: User who recorded the follow-up.
- `logged_by_role`: Defaults to `health_manager`.
- `logged_at`: Record creation timestamp.

The table records communication through channels such as letters, email, phone, and in-person contact.

Follow-up information is recorded by the system; the table does not itself send external communications.

### 2.12 Notifications

The `notifications` table stores notifications for users.

Important fields include:

- `notification_id`: UUID primary key.
- `recipient_user_id`: Notification recipient.
- Optional related equipment, fault, and resource-request references.
- `notification_type`: Notification classification.
- `message`: Notification content.
- `channel`: Defaults to `in_app`.
- `created_at`: Creation timestamp.
- Optional `delivered_at` and `read_at` timestamps.

The migration constrains the notification channel to `in_app`.

### 2.13 Audit Logs

The `audit_logs` table records actions performed within the system.

Important fields include:

- `audit_id`: UUID primary key.
- `actor_user_id`: Optional user associated with the action.
- `action`: Action performed.
- `entity_type`: Type of affected entity.
- `entity_id`: Optional affected entity UUID.
- `details`: Optional JSONB data containing additional details.
- `occurred_at`: Timestamp of the event.

The `entity_type` field is constrained to the supported audit entity types.

## 3. Relationships and Foreign Keys

The database uses foreign keys to maintain relationships between records.

The main relationships include:

- A department can be associated with multiple users and equipment records.
- A user can register equipment, report faults, upload documents, and perform other recorded actions.
- Equipment can have multiple documents and faults.
- A fault can have multiple assessments, status-history records, repair-verification records, and resource requests.
- A resource request can contain multiple request items and follow-up records.
- A user can receive multiple notifications.
- Audit records can reference the user responsible for an action.

Some relationships use composite foreign keys to enforce role and entity consistency. For example, engineer assignments reference both a user ID and role, ensuring that the assigned user has the expected biomedical engineer role.

The `users` and `departments` tables reference each other. The initial migration handles this circular dependency by adding the `users.department_id` foreign key after the relevant tables have been created.

The migration does not declare explicit `ON DELETE` or `ON UPDATE` actions for its foreign-key constraints.

## 4. Primary Keys and Identifiers

The tables use UUID primary keys for their main records.

The migration enables PostgreSQL's `pgcrypto` extension to support UUID generation through `gen_random_uuid()`.

UUID identifiers are used for users, departments, equipment, documents, faults, assessments, history records, repair records, requests, request items, follow-ups, notifications, and audit logs.

## 5. Enumerations and Database Constraints

The database uses enumerated values to restrict fields such as user roles, equipment statuses, fault statuses, and request types.

### 5.1 Native PostgreSQL Enum

The migration creates one native PostgreSQL enum type:

`user_role`

Its values are:

- `clinical_staff`
- `biomedical_engineer`
- `health_manager`

The type is used for role-related columns.

Other application enums are represented as string columns with database `CHECK` constraints rather than separate native PostgreSQL enum types.

### 5.2 Application Enum Values

| Enum | Values |
|---|---|
| AcquisitionType | `donated`, `purchased`, `transferred`, `unknown`, `other` |
| RegistrationStatus | `pending`, `approved`, `returned` |
| InstallationStatus | `unknown`, `not_installed`, `partially_installed`, `installed`, `commissioned` |
| ServiceStatus | `not_assessed`, `in_service`, `out_of_service`, `under_maintenance`, `not_installed`, `incomplete`, `retired` |
| DocumentType | `photo`, `manual`, `warranty`, `donation_letter`, `delivery_note`, `installation_report`, `calibration_certificate`, `other` |
| FaultSeverity | `low`, `medium`, `high`, `critical` |
| FaultStatus | `reported`, `assigned`, `under_inspection`, `awaiting_resources`, `under_repair`, `awaiting_verification`, `verified`, `closed`, `cancelled` |
| PriorityLevel | `low`, `medium`, `high`, `critical` |
| RecordType | `repair`, `functional_test`, `safety_test`, `calibration`, `performance_test`, `commissioning`, `release` |
| TestResult | `pass`, `fail`, `not_performed`, `not_applicable` |
| RequestType | `spare_parts`, `technical_support`, `replacement_resource`, `new_equipment` |
| RequestStatus | `pending`, `approved`, `rejected`, `returned`, `in_progress`, `resolved` |
| NotificationType | `fault_reported`, `fault_assigned`, `fault_status_changed`, `registration_submitted`, `registration_decided`, `request_submitted`, `request_decided`, `request_follow_up_due`, `equipment_returned_to_service` |
| FollowUpChannel | `letter`, `email`, `phone`, `in_person`, `other` |
| ReplyStatus | `no_reply`, `accepted`, `partly`, `declined` |
| AuditEntityType | `user`, `department`, `equipment`, `equipment_document`, `fault`, `fault_assessment`, `repair_verification_record`, `resource_request`, `notification` |

### 5.3 Important Integrity Constraints

The migration defines database checks to protect data consistency.

**Users**
- Email addresses must be normalized to lowercase and trimmed.
- Users other than health managers must have a department.
- Invitation acceptance and password fields must be consistent.
- Password-reset token hash and expiry must be present together.
- MFA cannot be enabled without an encrypted MFA secret.
- Token version cannot be negative.

**Departments**
- Responsible engineer role must be `biomedical_engineer`.

**Equipment**
- Asset tags must be unique.
- Approval status must be consistent with the presence of an approver and approval timestamp.
- Approver role must be `health_manager`.
- Warranty end date cannot precede the warranty start date.

**Faults**
- Severity and status must use supported values.
- Assigned engineer role must be `biomedical_engineer`.
- Faults in statuses other than `reported` and `cancelled` must have an assigned engineer.
- Closed and cancelled faults must have a closure timestamp.

**Fault assessments**
- Assessment values must fall within defined ranges.
- Severity factor must be between 1 and 4.
- Clinical criticality must be between 1 and 3.
- History factor must be between 0 and 3.
- Priority score must be between 2 and 12.
- Priority explanation cannot be empty.
- Assessor role must be `biomedical_engineer`.

**Repair verification**
- Authorization to return equipment to service is only allowed for a `release` record.
- A release timestamp must be present when service authorization is granted.
- Repair records must include work performed.
- Test records must use supported test results.
- Repair completion cannot precede repair start.
- The performer role must be `biomedical_engineer`.

**Resource requests**
- Non-pending requests must have a decision-maker and decision timestamp.
- Resolved requests must have a resolution timestamp.
- Decision-maker role must be `health_manager`.

**Request items**
- Requested quantity must be greater than zero.
- Approved quantity cannot exceed requested quantity.
- Fulfilled quantity cannot exceed approved quantity when an approved quantity is recorded.

**Request follow-ups**
- The next follow-up date cannot precede the sent date.
- Reply status and reply timestamp must be consistent.
- The logging user role must be `health_manager`.

**Notifications**
- Notification channel is restricted to `in_app`.

## 6. Indexes and Uniqueness

The migration defines unique constraints and partial unique indexes to prevent duplicate or conflicting records.

### 6.1 Unique Constraints

| Table | Unique field or combination |
|---|---|
| `users` | `email` |
| `users` | `(user_id, role)` |
| `departments` | `department_name` |
| `equipment` | `asset_tag` |
| `faults` | `client_report_id` |
| `faults` | `(fault_id, equipment_id)` |

The unique `(fault_id, equipment_id)` combination supports the composite foreign key used by repair verification records.

### 6.2 Partial Unique Indexes

| Index | Table | Condition | Purpose |
|---|---|---|---|
| `uq_assessment_current` | `fault_assessments` | `is_current` is true | Allows only one current assessment per fault. |
| `uq_record_one_release` | `repair_verification_records` | `authorized_for_service` is true | Allows only one authorized release record per fault. |

## 7. Database Functions and Triggers

The initial migration creates two PostgreSQL functions and three triggers.

### 7.1 Automatic Update Timestamps

The `set_updated_at()` function sets `NEW.updated_at` to the current database timestamp.

It is used by:

- `trg_equipment_updated_at`: Runs before updates to `equipment`.
- `trg_faults_updated_at`: Runs before updates to `faults`.

This ensures that the `updated_at` field is refreshed when these records are updated.

### 7.2 Release Test Validation

The `check_release_tests()` function validates repair verification records when `authorized_for_service` is true.

Before an equipment release is accepted, the function checks for the latest functional test and latest safety test for the same fault, considering tests performed on or before the release timestamp.

Both latest test results must be `pass`. If either required test is missing or does not have a passing result, the function raises a database check violation.

The function is attached to `repair_verification_records` through the `trg_record_release_tests` trigger, which runs before insert or update.

This provides a database-level safeguard against authorizing equipment for service without the required passing tests.

## 8. Fault Downtime View

The migration creates a database view named `fault_downtime`.

The view combines fault records with authorized repair-verification release records.

It exposes:

- `fault_id`
- `equipment_id`
- `out_of_service_at`
- `released_at`
- `downtime`
- `still_down`

The downtime calculation is:

`COALESCE(released_at, now()) - out_of_service_at`

The `still_down` field is true when no authorized release timestamp exists.

Only faults with a non-null `out_of_service_at` value are included.

This view provides a way to calculate equipment downtime without storing a separate downtime duration in the faults table.

## 9. Migration Management

Alembic manages database schema changes.

The initial migration is:

- Revision: `0001`
- Description: Create all Waliin tables, the `user_role` type, triggers, and the `fault_downtime` view.
- File: `alembic/versions/0001_create_all_tables.py`

The migration creates the PostgreSQL extension, enum type, tables, constraints, indexes, functions, triggers, and view.

### 9.1 Downgrade

The migration's downgrade procedure reverses the schema creation.

It first drops the `fault_downtime` view and the foreign key added separately to `users`. It then drops tables and indexes in dependency-safe order, followed by the database functions and `user_role` type.

The triggers are removed when their associated tables are dropped.

### 9.2 Migration Scope

The inspected Alembic versions directory contains the initial migration described above. Additional schema changes should be introduced through new Alembic revisions rather than by manually changing an already-applied migration.

## 10. Database Design Summary

The database structure supports the main equipment-management lifecycle:

1. Users and departments establish organisational ownership and access roles.
2. Equipment records capture registration, approval, installation, and service information.
3. Fault records capture equipment problems and their status history.
4. Fault assessments store technical findings and priority information.
5. Repair verification records document repair work and the tests required before release.
6. Resource requests and follow-ups record requests for additional support and external communication.
7. Notifications and audit logs provide user-facing updates and an activity record.

Database constraints, indexes, triggers, and foreign keys provide additional protection for data integrity and equipment-release requirements.