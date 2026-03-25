---
title: Roadmap & feature requests
nav_order: 7
---

# Roadmap & feature requests

Planned features and future work. Every item has been considered and explicitly
deferred — not forgotten. This page is updated as features are completed or
priorities change.

---

## Multi-tenancy

### Multiple tenant deployments
Deploy additional breed clubs (e.g. GSP Club SA) as separate tenants. The
multi-tenancy foundation is complete — adding a new tenant is a database insert
and DNS change, not a code change.

### Custom domain routing
Full multi-domain support in production (e.g. hprregistry.co.za, gspclub.co.za).
The backend already reads the `Host` header for tenant resolution. This is an
operational step, not a code change.

### Tenant self-service onboarding
Breed clubs provision their own tenant without developer involvement. Requires
billing integration to gate access.

### Database split-out per tenant
Move a high-traffic tenant to a dedicated Postgres instance. The infrastructure
is already designed for this — update one database row and the system routes
queries to the new instance. Zero code changes required.

### Global admin — cross-tenant queries
Platform admin can query across all tenant databases for aggregate stats and
cross-club pedigree research.

---

## Billing

### Stripe subscription management
Each tenant has a subscription. The billing status column and suspension check
are already in the system — wire up Stripe webhook events to control access.

### Usage-based billing
Charge per dog record, per active user, or per API call. Flat subscription is
simpler to start with.

---

## Monitoring & observability

### New Relic / Sentry integration
The observability interfaces (Logger, ErrorReporter, Metrics) are already in
place. Wiring up New Relic or Sentry is a one-file change — implement the
interface and swap it in at startup.

### Prometheus + Grafana
Self-hosted alternative. Implement `PrometheusMetrics` and expose a
`GET /metrics` endpoint.

### Uptime monitoring
`GET /health` is already built. Point an uptime service (UptimeRobot, Better
Uptime) at it.

### Error alerting
High-severity errors trigger Slack or email alerts. Implement an alerting
wrapper around the existing error reporter.

---

## Authentication

### Auth0 migration
Swap Clerk for Auth0. The auth abstraction layer makes this a one-file change
per repo — no handler, middleware, or component changes required.

### SSO / SAML
Enterprise clubs want SSO via their own identity provider. The auth abstraction
layer makes this transparent to the application once the auth provider supports
SAML.

---

## Registry features

### Pedigree tree visualisation
Interactive ancestor tree on dog profiles, configurable generations deep.
Requires a backend recursive query endpoint and a frontend tree component.

### Image upload
Upload dog images directly rather than linking to external URLs. Requires
object storage (S3, R2, or similar) and a presigned URL endpoint.

### Email notifications
Approval and rejection emails to kennel owners and users. Follows the same
interface pattern as error reporting — swap in a real email sender when ready.

### Kennel owner — approve ownership requests
Kennel owners can approve ownership requests for dogs in their kennel.
Currently admin-only. This is a permission assignment change, not a code change.

### Pedigree certificate export
Printable PDF pedigree certificate formatted like a kennel club certificate.
Requires the pedigree endpoint and PDF generation.

### Registry statistics page
Public page showing total dogs per breed, registrations per year, and active
kennels. Simple aggregate queries — purely additive.

### Public API
Read-only REST API for third parties to query approved records. Requires API
key management and rate limiting.

### Mobile app
React Native app for browsing, submitting dogs, and viewing pedigrees. The
REST API is the backend — a mobile app is a new frontend client.

---

## Operations

### Database migrations
Replace `make db-reset` with proper migration tooling before the first
production deployment with real user data.

### Zero-downtime deployments
Blue-green or rolling deployments. Worth doing before the first paying tenant
goes live.

### Automated backups
Scheduled Postgres backups with a tested restore procedure. Managed Postgres
providers handle this — document the procedure when production hosting is chosen.

### Rate limiting
Per-tenant, per-user rate limits. Requires Redis or an in-memory rate limiter.

### Breed management UI
Admin page to add/remove breeds without touching SQL. Build when non-technical
admins need to manage breeds.
