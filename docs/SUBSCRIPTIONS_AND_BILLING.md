# Subscriptions and Billing

## Purpose

FASRED Platform provides shared subscription, entitlement, billing and payment capabilities for the FASRED product ecosystem.

The platform coordinates the commercial relationship between customers, organisations and products. It establishes consistent rules for product access, subscription lifecycle management, payment processing and billing records.

## 1. Core Principles

Subscriptions and billing follow these principles:

- Product access is governed by explicit subscription and entitlement rules.
- Subscription status and payment status are distinct.
- Each financial transaction must be traceable to its intended customer, organisation, product and commercial purpose.
- Payment confirmation must be based on verified payment-provider evidence.
- Financial records must remain consistent, auditable and protected against unauthorised changes.
- Subscription changes must be reflected in applicable product-access decisions.
- Repeated requests and payment-provider callbacks must not create duplicate financial effects.
- Financial operations must preserve appropriate tenant boundaries.

## 2. Product Plans and Pricing

The platform manages product plans and their associated commercial terms.

Plan management covers:

- Plan creation and configuration
- Product-specific plan definitions
- Pricing and billing intervals
- Trial eligibility and duration
- Included features and usage entitlements
- Plan availability and retirement
- Plan changes and migration rules

Plans must define the product, applicable pricing, billing interval and included entitlements. Changes to plan definitions must not silently rewrite historical transactions or existing contractual records.

## 3. Trials

Trials allow eligible customers or organisations to evaluate a product under defined conditions.

Trial management covers:

- Eligibility and trial initiation
- Trial start and expiry
- Trial duration and applicable entitlements
- Trial status and access rules
- Conversion to a paid subscription
- Trial expiration and renewal eligibility

Trial rules must be clear and consistently enforced. Repeated registrations or subscription requests must not bypass applicable trial eligibility rules.

## 4. Subscription Lifecycle

The platform manages the subscription lifecycle, including:

- Subscription creation
- Activation
- Renewal
- Plan changes and upgrades
- Downgrades
- Cancellation
- Expiration
- Suspension
- Reactivation
- Termination

Each subscription must have a defined status and permitted state transitions.

Subscription changes must preserve the relationship between the customer, organisation, product, selected plan, billing terms and associated entitlement records.

## 5. Entitlements and Product Access

Entitlements determine which products, features or usage allowances an organisation can access under its commercial agreement.

The platform defines:

- Product-level access
- Plan-specific feature access
- Usage limits and quotas
- Trial entitlements
- Entitlement changes after plan modifications
- Access changes after renewal, cancellation, expiry or suspension
- Rules for any applicable grace periods

Entitlement decisions must be enforced by the appropriate server-side services. Frontend controls alone must not determine access to paid features.

Each product remains responsible for enforcing its domain-specific permissions in addition to the commercial entitlement supplied by the platform.

## 6. Billing and Financial Records

Billing services manage the records associated with subscription charges and other applicable commercial transactions.

Billing responsibilities include:

- Billing account association
- Invoice or billing-document records
- Charge calculation and applicable taxes
- Billing periods and due dates
- Payment allocations
- Outstanding balances
- Credits, refunds and adjustments
- Billing history
- Reconciliation records

Financial records must preserve transaction history and provide traceability between the original charge, subsequent adjustments and final financial outcome.

Corrections should use controlled adjustments or reversal records rather than silently changing historical financial transactions.

## 7. Payment Processing

The platform coordinates payment processing through supported payment providers.

Payment processing covers:

- Payment initiation
- Association of payments with the correct customer, organisation, product and billing record
- Provider transaction references
- Payment verification
- Successful, failed, pending and reversed outcomes
- Refund processing
- Payment status updates
- Reconciliation against provider records

A redirect to a success page or a client-submitted success message is not sufficient evidence of payment. The platform must verify payment through the provider's trusted verification mechanism.

Provider credentials and secret keys must be protected through secure configuration and secret-management practices.

## 8. Payment Callbacks and Idempotency

Payment providers may send repeated callbacks or deliver events out of order.

The platform must handle these conditions safely by:

- Verifying callback authenticity
- Validating transaction references and expected amounts
- Confirming currency and transaction ownership
- Preventing duplicate transaction processing
- Recording processed provider events
- Handling retries and delayed notifications
- Reconciling conflicting or incomplete payment states

Repeated callbacks for the same transaction must not create duplicate charges, duplicate subscription activations or duplicate entitlement changes.

## 9. Subscription and Payment State Coordination

Subscription status and payment status represent different aspects of the commercial lifecycle.

For example, a payment may be pending while a subscription remains awaiting activation. A cancellation may stop future renewals without erasing the history of previous successful payments.

The platform must define how payment outcomes affect subscription and entitlement state, including:

- Initial subscription activation
- Successful renewal
- Failed renewal
- Pending payment
- Cancellation and end-of-term access
- Expiration and suspension
- Refunds and chargebacks
- Payment reversals
- Reactivation after a resolved billing issue

State transitions must be controlled, traceable and consistent across the platform and participating products.

## 10. Renewals, Cancellations and Refunds

Renewal processing must follow the subscription's billing terms and applicable payment-provider rules.

Cancellation handling must define:

- Whether cancellation takes effect immediately or at the end of the billing period
- How future recurring charges are stopped
- When product entitlements change
- How the customer is notified
- How cancellation history is retained

Refund handling must record the original transaction, refund amount, reason where applicable, provider reference and resulting financial status.

A refund must not automatically imply that every associated subscription should be cancelled. The resulting subscription and entitlement changes must follow the applicable commercial rules.

## 11. Notifications

Subscription and billing events may trigger notifications, including:

- Trial commencement and expiry
- Subscription activation and renewal
- Payment success or failure
- Upcoming renewals and payment due dates
- Cancellation confirmation
- Suspension or expiration
- Refund updates
- Billing-document availability

Notifications must reflect the authoritative transaction or subscription state and must not independently determine whether payment succeeded or access should be granted.

## 12. Auditability and Financial Integrity

Commercial and financial operations must be traceable.

Relevant records include:

- Plan and pricing changes
- Subscription state transitions
- Entitlement changes
- Payment initiation and verification
- Provider transaction references
- Billing adjustments and refunds
- Administrative overrides
- Reconciliation outcomes

Access to financial and billing information must be restricted to authorised users and services. Sensitive payment information and provider credentials must be protected.

## 13. Tenant Isolation

Billing and subscription operations must enforce the correct customer and organisation boundaries.

The platform must validate that the requesting identity is authorised to access the relevant subscription, invoice, payment or financial record.

Provider callbacks must be associated with the correct transaction using trusted server-side records rather than a client-supplied organisation identifier alone.

Cross-tenant financial access must be explicitly authorised and auditable.

## 14. Testing and Operational Controls

Testing must cover:

- Subscription creation and state transitions
- Trial eligibility and expiry
- Plan changes and entitlement updates
- Successful, failed and pending payments
- Payment verification and callback authenticity
- Duplicate and out-of-order provider events
- Renewal, cancellation and refund workflows
- Financial record consistency
- Reconciliation discrepancies
- Unauthorised cross-tenant access
- Recovery from interrupted or partially completed operations

Financial workflows must support safe retries and provide a clear way to investigate unresolved transactions.

---

**Maintained by:** FASRED Technologies Ltd  
**Platform:** FASRED Platform  
**Website:** https://fasredtech.com/
