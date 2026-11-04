
# Problem Exploration

## 1. Introduction

Medical equipment plays an important role in the delivery of healthcare services. Public hospitals depend on equipment for diagnosis, treatment, patient monitoring and emergency care. However, equipment downtime remains a challenge in Ethiopian public hospitals, affecting the availability of essential healthcare services.

Waliin explores how better equipment records, structured fault reporting, equipment inspections and coordinated maintenance support can help hospitals manage their medical equipment and reduce downtime.

## 2. Problem Background

Studies conducted in Ethiopian public hospitals have reported significant levels of non-functional medical equipment.

At Tulu Bolo General Hospital, 85 out of 199 equipment items (42.7%) were non-functional. Across eight comprehensive specialized hospitals in Amhara, 572 out of 2,259 devices (25.32%) were non-functional.

Donated equipment presents additional challenges. At Jimma University Specialized Hospital, 99 out of 180 donated devices (55%) were not in use. Many lacked locally available spare parts, maintenance support or technical manuals.

Maintenance processes also face challenges. Equipment faults are sometimes communicated verbally rather than recorded through formal reporting processes. Incomplete equipment records and delayed spare-part procurement make it difficult for biomedical engineers to identify equipment needs and coordinate maintenance early.

These challenges contribute to prolonged equipment downtime and affect hospitals' ability to maintain equipment availability.

## 3. Problem Statement

Biomedical engineers in Ethiopian public hospitals often learn that medical equipment has a problem only after it has failed, while faults reported by clinical staff are frequently communicated verbally and not formally recorded.

Equipment records, inspection findings, repair histories and downtime information are often incomplete or difficult to track in one place. This makes it difficult for engineers to assess equipment condition, prioritise maintenance and prepare spare-part requests early.

For donated equipment and equipment whose supplier support has ended, unavailable spare parts and limited external support can leave machines out of service for weeks or months.

There is therefore a need for a coordinated system that improves equipment record-keeping, fault reporting, maintenance tracking and external support requests.

## 4. Stakeholders

Waliin considers the following stakeholders:

| Stakeholder | Interest and Involvement |
|---|---|
| Biomedical engineers | Register equipment, conduct inspections, review fault reports, assess equipment condition, prioritise maintenance, coordinate repairs and verify equipment before returning it to service. |
| Clinical staff | Report equipment faults, request new equipment for their departments and monitor the status of reports and requests. |
| Health managers / health officers | Oversee equipment resources, approve requests, coordinate with external partners and monitor equipment availability and downtime. |
| Patients | Benefit from the availability of functioning medical equipment for diagnosis and treatment. |
| Donors, suppliers and nearby hospitals | Receive requests for spare parts, repairs, replacements or new equipment. They are external partners and do not log in to Waliin. |

## 5. Existing Challenges

The problem exploration identified several challenges affecting medical equipment management in public hospitals.

### 5.1 Incomplete Equipment Records

Hospitals may lack reliable records of equipment models, installation dates, service history, equipment sources and technical specifications.

This makes it difficult to understand equipment condition, identify maintenance requirements and access relevant equipment information when needed.

### 5.2 Reactive Fault Reporting

Clinical staff often communicate equipment faults verbally.

Without a structured reporting process, faults can be forgotten, delayed or difficult to track. Biomedical engineers may also lack sufficient information to assess reported problems and determine the appropriate response.

### 5.3 Limited Maintenance Visibility

Biomedical engineers need access to inspection findings, fault histories, repair records and equipment condition to determine which machines require attention.

When this information is incomplete or scattered, it becomes difficult to assess equipment needs and coordinate maintenance activities.

### 5.4 Spare-Part and External Support Challenges

Hospitals may struggle to identify suppliers, obtain spare parts or coordinate external support, particularly for donated equipment.

Limited technical documentation, unavailable parts and unclear support arrangements can extend equipment downtime.

### 5.5 Inadequate Technical Requirements for New Equipment

New equipment requests may lack important technical requirements, including power specifications, spare parts, accessories, manuals, local maintenance support and training needs.

Incomplete specifications can make it difficult for hospital managers and external partners to assess equipment requirements.

### 5.6 Limited Request Follow-up

Requests sent to donors and suppliers can be difficult to track.

Without a structured follow-up process, hospital managers may have limited visibility into outstanding requests, external responses and the actions required to address equipment needs.

## 6. Impact of the Problem

Equipment downtime affects hospital operations and the availability of healthcare services.

The identified challenges can result in:

- Clinical staff having to find alternative equipment when machines fail.
- Patients experiencing delays in diagnosis or treatment.
- Biomedical engineers spending considerable time responding to breakdowns rather than identifying equipment needs early.
- Prolonged downtime while hospitals wait for spare parts or external support.
- Hospital managers having limited visibility into equipment condition, outstanding requests and maintenance needs.

These effects demonstrate the importance of improving equipment accountability, maintenance coordination and access to equipment information.

## 7. Proposed Solution

Waliin is a Progressive Web App (PWA) designed to help Ethiopian public hospitals manage medical equipment records, report faults, assess equipment condition, prioritise maintenance and coordinate requests for spare parts, repairs and replacements.

The system provides a shared platform for clinical staff, biomedical engineers and health managers.

Through Waliin:

- **Clinical staff** can report equipment faults and request new equipment for their departments.
- **Biomedical engineers** can register equipment, conduct quick inspections, assess equipment condition, review faults and record repairs.
- **Biomedical engineers** can prioritise equipment using recorded condition, inspection findings, fault status, maintenance history, clinical criticality, backup availability and their own assessments.
- **Health managers** can approve requests, generate request reports and track responses from donors and suppliers.
- **Equipment repair activities** can be documented and verified before equipment is marked as back in use.

The system maintains equipment histories and provides dashboards and reports to support maintenance planning and equipment availability monitoring.

### 7.1 Equipment Prioritisation Approach

Waliin uses a rule-based equipment prioritisation approach for the pilot.

Equipment prioritisation considers recorded equipment information, inspection findings, fault status, maintenance history, clinical criticality, backup availability and biomedical engineer assessments.

This supports structured maintenance prioritisation without introducing AI or machine learning-based failure prediction.

## 8. Project Scope

The project scope defines the functionality included in the pilot and the capabilities reserved for future development.

### 8.1 In Scope

The pilot focuses on:

- Equipment registration and equipment records.
- Quick equipment inspections.
- Fault reporting and fault review.
- Equipment risk assessment and priority lists.
- Rule-based equipment prioritisation.
- Maintenance actions and external support requests.
- New equipment requests and technical specifications.
- Repair records and return-to-service verification.
- Role-based dashboards and reports.
- User accounts, permissions and security.
- Offline fault reporting and inspection synchronisation.

### 8.2 Out of Scope

The following capabilities are excluded from the pilot:

- AI and machine learning for future failure prediction.
- Automatic maintenance decisions or automatic procurement.
- Live equipment monitoring through sensors.
- Automated email and SMS communication.
- External accounts for donors and suppliers.
- Full preventive maintenance scheduling.
- Procurement, finance and inventory management.
- Integration with MEMIS or other national systems.
- Multi-hospital operations.
- Storage of patient-identifiable information.

## 9. How the Problem Informs the System Design

The identified challenges inform the design of Waliin's main components and workflows.

| Identified Challenge | System Response |
|---|---|
| Incomplete equipment records | Equipment registration and model catalogue. |
| Verbal fault reporting | Structured fault reporting and review. |
| Limited equipment condition visibility | Quick inspections and equipment history. |
| Difficulty prioritising equipment | Engineer-led equipment risk assessment and rule-based priority lists. |
| Delayed spare-part requests | Maintenance actions and external support requests. |
| Inadequate technical specifications | New equipment requests with engineer-added technical requirements. |
| Limited request follow-up | Request tracking, replies and overdue follow-up flags. |
| Unverified repairs | Repair records and return-to-service verification. |
| Limited management visibility | Role-based dashboards and reports. |

The system is therefore designed around the actual workflows of clinical staff, biomedical engineers and health managers.

By providing structured equipment information, fault reporting, maintenance records and request tracking, Waliin aims to improve equipment accountability, support timely action and reduce avoidable downtime.

## 10. Related Documentation

- [Project Overview](overview.md)
- [System Architecture](architecture.md)
- [Frontend Documentation](frontend-documentation.md)
- [Backend Documentation](backend-documentation.md)
- [Database Design](database-design.md)
- [API Reference](api-reference.md)
- [Authentication and Security](authentication-and-security.md)
- [Testing](testing.md)
