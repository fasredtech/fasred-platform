# Identity and Access Management

## Purpose

This document defines the responsibilities and design principles for identity and access management within FASRED Platform.

The platform provides shared identity and access capabilities for supported FASRED products. Its goal is to establish consistent, secure and manageable access across the product ecosystem while preserving product-specific authorisation requirements.

This document describes the intended platform scope. Individual capabilities must be verified against the current implementation before being considered operational.

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
- Security events and auditability
- Integration with supported FASRED products

## 1. User Registration and Account Lifecycle

The platform is intended to support controlled account creation and lifecycle management, including:

- Registration and account creation
- Input validation and duplicate-account handling
- Email or other configured identity verification
- Account activation and status management
- Profile and identity updates
- Password creation, change and recovery where password authentication is supported
- Account suspension, deactivation and reactivation according to authorised policies
- Account closure and associated data-retention requirements

Registration must not automatically grant unrestricted access to every product or organisation. Access should follow the applicable identity, organisation, subscription and authorisation rules.

## 2. Authentication and Sessions

Authentication establishes the identity of the user or service requesting access.

The platform should enforce:

- Secure credential verification
- Appropriate session or token lifecycle controls
- Expiration and revocation of sessions or credentials where supported
- Protection against brute-force attempts and credential abuse
- Secure account recovery
- Consistent handling of authentication failures
- Appropriate controls for privileged accounts and sensitive operations

Authentication success alone must not be treated as proof that a user is authorised to perform every requested action.

## 3. Single Sign-On (SSO)

SSO is intended to allow users to access supported FASRED products through a common identity experience without unnecessarily repeating authentication.

The implementation should define:

- Supported identity protocols and flows
- Trusted applications and registered clients
- Redirect URI validation
- Token issuance, validation and expiration
- Audience, issuer and signature verification where applicable
- Session establishment and termination behaviour
- Logout behaviour across the identity service and participating applications
- Safe handling of authentication errors and failed callbacks

Each participating product must validate the identity and access information it receives according to the platform's documented integration contract.

## 4. Multi-Factor Authentication (MFA)

MFA provides an additional authentication factor beyond a primary credential.

The platform's MFA design should define:

- Supported authentication factors
- MFA enrolment and verification
- Recovery procedures
- Factor replacement and removal
- Policies for privileged accounts and sensitive operations
- Protection against repeated verification attempts
- Auditing of enrolment, recovery and security-sensitive changes

MFA recovery must not create an easier route around the security controls it is intended to strengthen.

Only the factors and policies actually implemented should be documented as available to users.

## 5. Organisations and Membership

The platform is intended to support users who may belong to one or more organisations, subject to the applicable product and account model.

Access administration should establish:

- Organisation membership and membership status
- Invitations and membership acceptance where supported
- Assignment and removal of organisation-level roles
- Rules for organisation administrators
- Membership changes and access revocation
- Appropriate separation between personal accounts and organisation resources

Membership in one organisation must not automatically grant access to another organisation's resources.

## 6. Roles, Permissions and Authorisation

Authorisation determines what an authenticated identity is permitted to do.

The platform should support clearly defined and enforceable access policies, including:

- Least-privilege access
- Explicit permission checks for protected operations
- Role assignment and management
- Separation of administrative responsibilities where appropriate
- Permission changes and revocation
- Denial by default when a required permission cannot be established
- Server-side enforcement rather than reliance on frontend visibility alone

Platform-level access controls and product-specific business permissions must have clear ownership boundaries.

## 7. Product Integration

FASRED products may use platform identity services through supported and documented integration interfaces.

Products include:

- FASPEP — Digital examinations and assessment
- FASOSH — Healthcare operations and management
- FASWORK — Asset and maintenance lifecycle management

Integration contracts should define how identity is established, how tokens or sessions are validated, how organisation context is represented and how access failures are handled.

Each product remains responsible for enforcing its domain-specific permissions and business rules. A shared identity service must not bypass those controls.

## 8. Security Events and Auditability

Identity-related security events should be recorded where supported and appropriate, including:

- Successful and failed authentication
- Account recovery and security-setting changes
- MFA enrolment and recovery
- Session or token revocation
- Privilege and role changes
- Organisation membership changes
- Administrative actions affecting access

Audit records should contain sufficient information for investigation without unnecessarily exposing passwords, authentication secrets, access tokens or other sensitive credentials.

Access to audit records must itself be controlled.

## 9. Notifications

Identity-related notifications may include registration verification, account recovery, authentication alerts and important account-security changes.

Notifications should use verified destinations and appropriate safeguards. Sensitive authentication information must not be exposed through ordinary notification content.

Notification delivery, retries and delivery status should follow the platform's implemented notification capabilities.

## 10. Operational and Security Requirements

Identity and access services should be developed and operated with attention to:

- Secure configuration and secret management
- Appropriate rate limiting and abuse prevention
- Monitoring of authentication failures and security events
- Reliable access revocation
- Automated testing of authentication and authorisation boundaries
- Protection against cross-tenant access
- Safe error handling
- Backup, recovery and incident-response procedures appropriate to the service

These are engineering requirements and principles, not assertions that every control is already implemented.

## 11. Implementation Status

For each capability, maintain a clear status:

- **Implemented** — verified in the current codebase and supported by relevant tests or operational evidence.
- **Partially implemented** — some components exist, but the full capability is incomplete.
- **Planned** — intended but not yet implemented.
- **Needs verification** — the current implementation or operational state has not been confirmed.

Do not describe a capability as production-ready solely because it is documented.

## 12. Change Management

Changes affecting identity, authentication, SSO, MFA or authorisation should be reviewed for security impact and backward compatibility.

Changes should include appropriate automated tests, migration considerations and documentation updates. Security-sensitive changes should receive additional scrutiny before deployment.

---

**Maintained by:** FASRED Technologies Ltd  
**Platform:** FASRED Platform  
**Website:** https://fasredtech.com/
