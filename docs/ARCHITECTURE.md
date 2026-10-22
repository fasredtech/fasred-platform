
# FASRED Platform Architecture

## 1. Purpose

FASRED Platform is the shared technical foundation for FASRED Technologies products. It provides common services for identity, access management, organisation management, subscriptions, billing, payments, notifications, and product integrations.

The architecture must support secure, reliable operation across multiple products and organisations while allowing each product to evolve independently within clearly defined boundaries.

## 2. Architecture Goals

The platform architecture must:

- Provide consistent identity and access experiences across FASRED products.
- Enforce organisation and tenant isolation.
- Centralise shared capabilities without absorbing product-specific business logic.
- Support secure integration between the platform and its products.
- Maintain reliable subscription, entitlement, billing, and payment workflows.
- Provide traceability for security-sensitive and financial operations.
- Support maintainable development, testing, deployment, and future scaling.
- Minimise unnecessary duplication of shared capabilities across products.

## 3. Logical Architecture

The platform is organised around the following logical responsibilities.

### 3.1 Product and Client Interfaces

Provide the interfaces through which users, organisation administrators, platform administrators, and integrated products access platform capabilities.

Interfaces must respect the same authentication, authorisation, tenant-context, and validation requirements as the underlying services.

### 3.2 Identity and Access Management

Responsible for:

- User accounts and account lifecycle.
- Authentication and session management.
- Single sign-on (SSO).
- Multi-factor authentication (MFA).
- Organisation membership and role assignments.
- Permission evaluation and access decisions.
- Identity-related security events.

### 3.3 Organisation and Tenant Management

Responsible for:

- Organisation registration and lifecycle.
- Organisation membership and administrative roles.
- Tenant identity and context.
- Organisation-level settings and configuration.
- Product access associated with an organisation.
- Tenant-scoped administrative operations.

### 3.4 Subscription, Billing, and Payments

Responsible for:

- Plans, pricing, and subscription lifecycle.
- Trials, renewals, cancellations, and applicable refunds.
- Product entitlements and subscription access.
- Billing records and payment reconciliation.
- Payment-provider integration and callback processing.
- Financial auditability and transaction consistency.

### 3.5 Notifications and Event Processing

Responsible for:

- Account, security, organisation, subscription, billing, and payment notifications.
- Notification templates and channel configuration.
- Internal events used to coordinate platform workflows.
- Delivery attempts, retries, and failure handling.
- Duplicate-event protection and operational visibility.

### 3.6 Integration Interfaces

Provide controlled interfaces through which FASRED products and approved external services communicate with platform capabilities.

Integration contracts must define authentication, permissions, request validation, response formats, error handling, versioning, and relevant tenant context.

### 3.7 Data and Persistence

Each logical responsibility must have clearly defined ownership of its data and business rules.

Data access must enforce tenant boundaries, integrity constraints, and appropriate access controls. Cross-domain operations must use explicit service interfaces and documented workflow rules rather than unrestricted access to another domain's internal data.

### 3.8 Operations and Observability

Provide the operational foundations needed to run and maintain the platform, including:

- Configuration and secret management.
- Application logs and error reporting.
- Health checks and service monitoring.
- Security and administrative audit trails.
- Backup and recovery procedures.
- Deployment and environment management.
- Operational alerts and incident investigation.

## 4. Platform and Product Boundaries

FASRED Platform provides shared services. Individual products remain responsible for their own domain-specific workflows and records.

### FASPEP

FASPEP is responsible for examination and assessment workflows, including academic structures, examination delivery, responses, marking, moderation, and results.

FASRED Platform provides the shared identity, organisation, access, subscription, billing, and notification capabilities required by FASPEP.

### FASOSH

FASOSH is responsible for healthcare operations and clinical workflows, including patient care, clinical records, hospital operations, and healthcare-specific permissions and controls.

FASRED Platform provides shared identity, organisation, access, subscription, billing, and integration services. Clinical data and clinical workflow rules remain within the healthcare product's domain.

### FASWORK

FASWORK is responsible for maintenance, asset management, work orders, inventory, and related operational workflows.

FASRED Platform provides shared identity, organisation, access, subscription, billing, and notification capabilities. Maintenance and asset-management rules remain within FASWORK's domain.

## 5. Identity and Trust Boundaries

Every protected request must be authenticated or explicitly authorised through a defined trusted mechanism.

Authentication establishes identity; authorisation determines whether an action is permitted.

The architecture must enforce:

- Least-privilege access.
- Server-side permission checks.
- Verified identity and token claims.
- Explicit organisation and tenant context.
- Separation of platform administration from organisation administration.
- Controlled service-to-service authentication.
- Secure handling of sessions, tokens, credentials, and secrets.
- Auditability for sensitive administrative and security operations.

A client-supplied organisation identifier, role, user identifier, or product entitlement must not be accepted as proof of authority.

## 6. Tenant Isolation

Tenant context must be established and validated for every operation involving organisation-scoped resources.

The architecture must prevent users, administrators, services, and products from accessing another tenant's records without explicit, authorised cross-tenant privileges.

Tenant isolation applies to:

- Database queries and mutations.
- API endpoints and background jobs.
- File and object storage.
- Cached data and derived results.
- Search and reporting operations.
- Notifications and event processing.
- Exports, imports, and administrative tools.
- Logs and audit records containing tenant information.

Cross-tenant administrative access must be explicitly permissioned, limited to its intended purpose, and auditable.

## 7. API and Integration Contracts

Platform APIs must provide stable, documented contracts for supported consumers.

Each contract must define:

- Endpoint purpose and supported operations.
- Authentication and authorisation requirements.
- Required tenant and organisation context.
- Request and response schemas.
- Validation and error responses.
- Pagination and filtering where applicable.
- Idempotency requirements for repeatable or consequential operations.
- Versioning and compatibility expectations.
- Rate limits and abuse controls where appropriate.

Changes to shared contracts must consider the impact on all consuming products. Breaking changes require a managed migration path.

## 8. Workflow Coordination and Consistency

Some business workflows cross multiple platform responsibilities. Examples include account registration, organisation onboarding, subscription activation, payment confirmation, renewal, and account or subscription notifications.

These workflows must define:

- The initiating action or event.
- The authoritative owner of each state transition.
- Preconditions and validation rules.
- Successful and failed outcomes.
- Retry and recovery behaviour.
- Duplicate-request and duplicate-event handling.
- Notifications and audit events.
- Reconciliation procedures for incomplete or conflicting states.

Payment confirmation, entitlement changes, and subscription state transitions must remain consistent. External provider callbacks must be authenticated and processed safely, with idempotent handling of repeated events.

Where a workflow spans independent systems, the architecture must account for partial failure and eventual completion rather than assuming every step succeeds together.

## 9. Events and Background Processing

Background processing may be used for notifications, integration events, reconciliation, and other tasks that do not need to complete within the initiating request.

Background jobs and event handlers must:

- Validate their input and originating context.
- Preserve required tenant and correlation identifiers.
- Avoid duplicate consequential actions.
- Use bounded retries and explicit failure handling.
- Record relevant outcomes for investigation.
- Avoid exposing sensitive information in logs or event payloads.

Events must have clear ownership, documented meaning, and defined consumer expectations.

## 10. Data Ownership and Integrity

Every domain must define which service is authoritative for its records and state transitions.

The architecture must preserve:

- Referential and business-rule integrity.
- Tenant-scoped uniqueness where required.
- Consistent subscription and entitlement state.
- Reliable financial records and reconciliation.
- Controlled access to sensitive data.
- Appropriate retention and deletion rules.
- Auditable changes to important records.

Consumers must use supported interfaces rather than independently modifying another domain's authoritative records.

## 11. Configuration and Secrets

Environment-specific settings must be managed separately from application code.

Credentials, signing keys, payment-provider secrets, database credentials, and other sensitive configuration must not be committed to source control or exposed in client-side code.

Access to production secrets must be restricted to authorised services and personnel. Secret rotation and recovery procedures must be defined for critical credentials.

Security-sensitive configuration changes must be controlled and traceable.

## 12. Reliability and Operations

The platform must support reliable operation through:

- Defined health and readiness checks.
- Structured, useful logs and correlation identifiers.
- Monitoring of authentication, integration, payment, and notification failures.
- Database backup and recovery procedures.
- Controlled deployments and rollback procedures.
- Resource and connection management.
- Documented incident response and recovery procedures.
- Capacity planning as product usage grows.

Operational design must account for external dependencies, network failures, unavailable providers, and temporary service interruptions.

## 13. Testing Strategy

Testing must cover both individual responsibilities and end-to-end platform workflows.

Required testing areas include:

- Unit tests for business rules and validation.
- API contract and integration tests.
- Authentication, session, SSO, and MFA tests.
- Permission and role enforcement tests.
- Tenant-isolation tests across relevant access paths.
- Subscription, payment, entitlement, and reconciliation tests.
- Idempotency, retries, and failure-recovery tests.
- Notification and event-processing tests.
- Regression tests for consuming products.
- Deployment, backup, and recovery procedures.

Security and tenant-isolation tests must exercise both permitted and prohibited access paths.

## 14. Change Management

Changes to shared platform capabilities must consider their impact on all dependent products and integrations.

Changes must preserve documented contracts, access-control rules, tenant boundaries, data integrity, and operational requirements.

Database changes, API changes, configuration changes, and migrations must have defined deployment and recovery procedures appropriate to their risk.

Architecture decisions that materially affect security, reliability, integration, or data ownership should be documented so future development remains consistent.

## 15. Guiding Principle

FASRED Platform should make shared capabilities consistent and dependable across FASRED products while allowing each product to deliver its own specialised value.

The platform is the common foundation; FASPEP, FASOSH, and FASWORK remain distinct products built on that foundation.
