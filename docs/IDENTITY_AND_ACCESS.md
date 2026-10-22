# Identity and Access Management

## Purpose

FASRED Platform provides the shared identity and access foundation for the FASRED product ecosystem. It centralises user identity, authentication and access-management capabilities to deliver a consistent, secure experience across products.

The platform establishes common identity and security controls while allowing each product to enforce its own domain-specific permissions and business rules.

## Scope

Identity and access management covers:

- User registration and account lifecycle management
- Authentication and session management
- Single sign-on (SSO)
- Multi-factor authentication (MFA)
- Organisation membership and access administration
- Roles, permissions and authorisation
- Credential and account security
- Identity-related notifications
- Security events and audit trails
- Integration with FASRED products

## 1. User Registration and Account Lifecycle

The platform manages the user account lifecycle, including:

- User registration and account creation
- Input validation and duplicate-account prevention
- Identity and contact verification
- Account activation and status management
- Profile and identity updates
- Password creation, changes and recovery
- Account suspension, deactivation and reactivation
- Account closure and associated data-retention requirements

Account creation does not automatically grant access to every organisation or product. Access is governed by identity verification, organisation membership, permissions and applicable product entitlements.

## 2. Authentication and Session Management

Authentication establishes the identity of a user or service requesting access.

The platform enforces:

- Secure credential verification
- Controlled session and token lifecycles
- Session expiration and revocation
- Protection against brute-force attacks and credential abuse
- Secure account recovery
- Consistent handling of authentication failures
- Additional safeguards for privileged accounts and sensitive operations

Authentication and authorisation are separate controls. A successfully authenticated identity must still be authorised to perform the requested operation.

## 3. Single Sign-On (SSO)

SSO provides a common authentication experience across participating FASRED products, reducing unnecessary repeated logins while maintaining appropriate security boundaries.

The platform defines:

- Supported identity protocols and authentication flows
- Trusted applications and registered clients
- Strict redirect URI validation
- Token issuance, validation and expiration
- Issuer, audience and signature verification
- Session establishment and termination
- Logout behaviour across the identity service and participating applications
- Secure handling of authentication errors and callback failures

Participating products validate identity assertions and tokens according to the platform's integration contract. They must not accept untrusted identity information or bypass their own authorisation controls.

## 4. Multi-Factor Authentication (MFA)

MFA adds an additional authentication factor to strengthen account security.

The platform's MFA controls cover:

- Factor enrolment and verification
- Supported authentication factors
- Recovery and factor replacement
- Factor removal and security-setting changes
- Policies for privileged accounts and sensitive operations
- Protection against repeated verification attempts
- Audit records for enrolment, recovery and security-sensitive changes

MFA recovery must maintain appropriate identity verification and must not provide an easier route around the security controls it is intended to strengthen.

## 5. Organisations and Membership

The platform manages organisation membership and the relationship between user identities and organisational access.

Membership management includes:

- Organisation membership and membership status
- Invitations and membership acceptance
- Assignment and removal of organisation-level roles
- Organisation administrator responsibilities
- Membership changes and access revocation
- Separation of personal accounts from organisation resources

Membership in one organisation does not grant access to another organisation's resources.

## 6. Roles, Permissions and Authorisation

Authorisation determines which operations an identity is permitted to perform.

The platform establishes consistent access-control principles, including:

- Least-privilege access
- Explicit permission checks for protected operations
- Role assignment and management
- Separation of administrative responsibilities
- Permission changes and revocation
- Denial by default when authorisation cannot be established
- Server-side enforcement of access policies

Platform-level permissions govern shared platform operations. Product-specific permissions govern domain workflows and resources within each product.

Frontend visibility is not an authorisation mechanism. Every protected operation must be enforced at the appropriate server-side boundary.

## 7. Product Integration

FASRED products integrate with shared platform identity services through defined interfaces.

The product ecosystem includes:

- **FASPEP** — Digital examinations and assessment.
- **FASOSH** — Healthcare operations and management.
- **FASWORK** — Asset and maintenance lifecycle management.

Integration contracts define identity establishment, token or session validation, organisation context, access-control expectations and authentication failure handling.

Each product retains responsibility for its domain-specific authorisation, business rules and protected resources. Shared authentication does not override product-level security controls.

## 8. Security Events and Audit Trails

Identity-related security events are recorded to support accountability, monitoring and investigation.

Events include:

- Successful and failed authentication
- Account recovery and security-setting changes
- MFA enrolment and recovery
- Session or token revocation
- Privilege and role changes
- Organisation membership changes
- Administrative actions affecting access

Audit records must contain sufficient information for investigation without exposing passwords, authentication secrets, access tokens or other sensitive credentials.

Access to audit records is itself controlled and auditable.

## 9. Identity Notifications

The platform coordinates identity-related notifications, including registration verification, account recovery, authentication alerts and important account-security changes.

Notifications must use appropriately verified destinations and protect sensitive information. Authentication secrets and access credentials must never be exposed through ordinary notification content.

Notification processing must handle delivery status, retries and failures according to the platform's notification architecture.

## 10. Operational Security

Identity and access services are developed and operated with the following controls:

- Secure configuration and secret management
- Rate limiting and abuse prevention
- Monitoring of authentication failures and security events
- Reliable access revocation
- Automated authentication and authorisation tests
- Protection against cross-tenant access
- Safe error handling
- Appropriate backup, recovery and incident-response procedures

## 11. Change Management

Changes affecting identity, authentication, SSO, MFA or authorisation require security review and backward-compatibility assessment.

Changes must include appropriate automated tests, migration planning and documentation updates. Security-sensitive changes receive additional scrutiny before deployment.

---

**Maintained by:** FASRED Technologies Ltd  
**Platform:** FASRED Platform  
**Website:** https://fasredtech.com/
