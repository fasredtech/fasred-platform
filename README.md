# FASRED Platform

**The shared technology foundation powering FASRED products.**

FASRED Platform is the central platform behind the FASRED product ecosystem. It provides shared services for identity, authentication, organisation management, access control, subscriptions, billing, payments, notifications and product integration.

The platform is designed to help FASRED products operate through consistent shared services rather than independently rebuilding the same capabilities in every product.

## Purpose

FASRED Platform provides a common foundation for managing users, organisations, access, subscriptions and shared operational services across supported FASRED products.

Its architectural direction prioritises security, tenant isolation, reliability, maintainability, accessibility and the ability to support products and organisations of different sizes.

## Core Platform Responsibilities

### Identity and Access Management

- User registration and account lifecycle management
- Authentication and session management
- Single sign-on (SSO)
- Multi-factor authentication (MFA)
- Roles, permissions and access-control policies
- Organisation membership and access administration

### Organisation and Tenant Management

- Organisation registration and management
- Tenant-aware service access
- Organisation membership and product access
- Separation of tenant data and operations
- Support for product-specific organisational structures

### Subscriptions and Billing

- Subscription lifecycle management
- Plans, entitlements and product access
- Trials and subscription status management
- Billing records and payment coordination
- Payment-provider integration
- Subscription-related notifications and status changes

### Notifications

- Account and security notifications
- Registration and authentication-related communications
- Subscription, billing and payment notifications
- Product and organisation event notifications
- Delivery status and notification lifecycle management, where supported

### Shared Services and Integration

- Common services used by multiple FASRED products
- Defined integration boundaries between the platform and products
- Consistent identity and access patterns
- Shared configuration and operational capabilities
- Integration interfaces for supported product workflows

## Relationship with FASRED Products

FASRED Platform provides shared capabilities to the wider product ecosystem. Each product remains responsible for its own domain-specific workflows and business rules.

- **FASPEP** — Digital examinations and assessment.
- **FASOSH** — Healthcare operations and management.
- **FASWORK** — Asset and maintenance lifecycle management.

The platform and each product should maintain clear ownership boundaries, with integrations based on explicitly defined and supported interfaces.

## Security and Architecture Principles

The platform's design and development should prioritise:

- Secure authentication and authorisation
- Least-privilege access
- Tenant isolation and controlled cross-tenant access
- Protection of credentials, secrets and sensitive data
- Auditable security-sensitive operations
- Validated subscription entitlements and product access
- Reliable handling of payment and subscription state changes
- Clear service boundaries and maintainable interfaces
- Appropriate monitoring, testing, backup and recovery practices

These principles describe the intended engineering direction; individual controls and operational guarantees must be verified against the implementation.

## Development and Repository Scope

This repository is the source-code home for the shared FASRED Platform, including its platform-specific services, interfaces, configuration and supporting tests as applicable to the actual implementation.

Product-specific business logic belongs in the relevant product repository unless a capability is deliberately designed and governed as a shared platform service.

Implementation documentation should identify which capabilities are implemented, partially implemented, planned or awaiting verification. Documentation must not be treated as proof that a feature is operational.


## Documentation

- [Platform Architecture](docs/ARCHITECTURE.md) — Overall architecture, service boundaries, integrations, reliability, and operations.
- [Identity and Access Management](docs/IDENTITY_AND_ACCESS.md) — Accounts, authentication, SSO, MFA, roles, permissions, and identity security.
- [Organisation and Tenancy](docs/ORGANISATION_AND_TENANCY.md) — Organisation lifecycle, tenant context, data isolation, and product access.
- [Subscriptions and Billing](docs/SUBSCRIPTIONS_AND_BILLING.md) — Plans, trials, subscriptions, entitlements, billing, payments, and renewals.
- [Notifications and Integrations](docs/NOTIFICATIONS_AND_INTEGRATIONS.md) — Notification delivery, event processing, integration contracts, retries, and reliability.


## Security Notice

This repository is private because the platform contains security-sensitive shared infrastructure.

Never commit passwords, API keys, private certificates, production credentials, customer information, database dumps or unredacted environment files. Use approved secret-management and configuration practices.

## Company

**FASRED Technologies Ltd**

Website: https://fasredtech.com/

**Technology Engineered for Impact.**
