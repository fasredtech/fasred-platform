# Organisation Management and Tenant Isolation

## Purpose

FASRED Platform provides shared organisation and tenancy management across the FASRED product ecosystem.

It manages organisation identity, membership and organisational access context. Each product enforces the appropriate data-access rules and business permissions for its own domain.

The platform establishes consistent organisational boundaries while enabling products to serve organisations of different sizes, structures and operational requirements.

## 1. Core Principles

Organisation and tenancy management follows these principles:

- Every organisation has a unique identity and defined lifecycle.
- Users receive access through authorised account, membership and permission rules.
- Tenant boundaries are enforced on the server side.
- An organisation cannot access another organisation's private resources without explicitly authorised cross-tenant access.
- Organisation context is established from trusted and validated identity and access information.
- Product-specific data and workflows remain under the responsibility of the relevant product.
- Organisation lifecycle changes propagate to relevant platform services and products.

## 2. Organisation Lifecycle

The platform manages the organisation lifecycle, including:

- Organisation registration and creation
- Organisation profiles and configuration
- Ownership and administrator assignment
- Membership invitations and onboarding
- Organisation activation and suspension
- Administrator and membership changes
- Organisation closure and deactivation
- Data-retention and closure requirements

Organisation states, permitted transitions and approval requirements are governed by defined business rules.

Creating an organisation does not automatically grant unrestricted administrative privileges or access to every product.

## 3. User Membership

A user may belong to multiple organisations, subject to the account and membership model.

Membership management covers:

- Membership creation and verification
- Invitation and approval workflows
- Membership status and lifecycle
- Role and permission assignment
- Membership changes and audit records
- Access revocation when membership ends
- Pending and expired invitations

A user's global platform identity is distinct from their membership in an organisation and their permissions within a particular product.

## 4. Tenant Identity and Context

Every tenant-scoped operation must resolve and validate the correct organisation context before accessing protected resources.

The platform defines:

- The authoritative tenant identifier
- How tenant context is established and validated
- How tenant context is propagated between trusted services
- How tenant context is enforced in database queries and resource access
- How background jobs and asynchronous events preserve tenant context
- How tenant context is represented in logs and audit records without exposing sensitive information

A tenant identifier supplied by a client is not proof of permission to access that tenant.

## 5. Data Isolation

Tenant isolation is enforced at the resource-access boundary, not merely through frontend filtering.

The platform and its products enforce appropriate isolation across:

- Database reads, inserts, updates and deletions
- Organisation-scoped files, exports and reports
- Background jobs and asynchronous processing
- Caches and search indexes
- Analytics and reporting data
- APIs and service-to-service communication
- Administrative and support operations

Every protected resource access must validate the requesting identity, organisation context and applicable permissions.

Tenant isolation must remain consistent across all access paths, including direct API requests, indirect service calls, background processing and administrative workflows.

Automated tests cover authorised and unauthorised cross-tenant access, including attempts to read, modify or delete another organisation's resources.

## 6. Platform and Product Responsibilities

FASRED Platform manages shared organisation identity, membership and tenancy capabilities.

Each product remains responsible for its domain data, workflows and business-level authorisation.

Examples include:

- **FASPEP:** School and examination organisation workflows, academic structures and examination data.
- **FASOSH:** Healthcare organisation structures, facilities, clinical workflows and healthcare records.
- **FASWORK:** Operational sites, assets, maintenance workflows and maintenance records.

These responsibilities establish clear architectural boundaries. Product-specific business logic belongs to the relevant product, while genuinely shared capabilities belong to the platform.

A successful platform login does not, by itself, authorise access to product-specific resources.

## 7. Product Access and Subscription Entitlements

Organisation membership, product access, subscription status and feature entitlements are separate controls.

Access decisions consider:

- Whether the user is authenticated
- Whether the user is authorised within the organisation
- Whether the organisation has access to the requested product
- Whether the relevant capability is included in the applicable entitlement
- Whether the user's role permits the requested operation

An active subscription does not grant every organisation member unrestricted access. Organisation membership alone does not grant access to every product or paid capability.

These controls must be enforced at the relevant server-side access boundaries.

## 8. Administrative and Support Access

Administrative access across organisations is governed by explicit permissions and accountability controls.

The platform defines:

- Roles permitted to administer organisations
- The conditions under which support personnel may access tenant resources
- Approval and authorisation for exceptional cross-tenant access
- Additional verification for elevated access
- Audit records for sensitive administrative actions
- Revocation of temporary or exceptional access
- Prevention of unauthorised administrative actions

Administrative privileges must be limited to the responsibilities assigned to each role. Cross-tenant access must be explicitly authorised and auditable.

## 9. Lifecycle Changes and Service Coordination

Organisation changes may affect authentication, membership, subscriptions, notifications and product access.

The platform coordinates relevant changes, including:

- Organisation activation and suspension
- Membership creation and removal
- Role and permission changes
- Subscription changes
- Product-access changes
- Organisation closure

Asynchronous processing must account for retries, duplicate events, partial failures and eventual consistency.

Access revocation and organisation-state changes must be handled according to defined transition rules so that stale permissions do not continue to grant access.

## 10. Auditability and Privacy

Organisation and tenant events are recorded to support accountability, security monitoring and investigation.

Auditable events include:

- Organisation creation and lifecycle changes
- Membership and role changes
- Administrative actions
- Product-access and entitlement changes
- Exceptional cross-tenant access
- Relevant access-control failures

Audit records must protect confidential information, maintain appropriate access controls and support applicable retention requirements.

## 11. Testing and Verification

Tenant isolation is tested across the complete resource-access lifecycle.

Testing covers:

- Attempts to read another tenant's records
- Attempts to modify or delete another tenant's records
- Access using tenant identifiers supplied by clients
- File, export and report access
- Background jobs and asynchronous processing
- Cache and search behaviour
- Role changes and membership revocation
- Organisation suspension and product-access changes
- Administrative exceptions and audit logging

Tests must exercise both authorised access and prohibited cross-tenant access. Failures must be investigated and corrected before the affected changes are released.

---

**Maintained by:** FASRED Technologies Ltd  
**Platform:** FASRED Platform  
**Website:** https://fasredtech.com/
