# API Design

This document describes the API design principles and conventions used by NesFlo. It complements the architecture by defining stable, versioned contracts that clients and integrations depend upon.

---

## Principles

- API-First: All platform capabilities are exposed via documented REST endpoints.
- Versioned: Use path-based versioning (`/api/v1/`) to allow non-breaking evolution.
- Consistent: Standard request/response formats, pagination, sorting, and error models.
- Secure: All protected endpoints require authentication and follow least-privilege access.
- Discoverable: Provide OpenAPI specs for each service.

---

## Authentication & Authorization

- Primary: JWT bearer tokens with short TTLs.
- Secondary: API keys for service-to-service communication.
- OAuth2: Planned for delegated integrations.
- RBAC: Enforce role and permission checks at the API layer.

---

## Endpoint Conventions

- Resource-based URLs (plural): `/api/v1/workflows`, `/api/v1/organizations/{id}/connectors`
- Use HTTP verbs: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`.
- Consistent error model: return `4xx` or `5xx` with JSON body `{ "code": "ERR_CODE", "message": "...", "details": { ... } }`.
- Support `Accept`/`Content-Type` negotiation for JSON and other formats where appropriate.

---

## Pagination & Filtering

- Use cursor-based or keyset pagination for large result sets.
- Provide filtering via query parameters and a standardized `filter` syntax where necessary.

---

## Rate Limiting & Quotas

- Enforce tenant-aware rate limits at the API Gateway.
- Provide headers with remaining quota and reset time.

---

## Webhooks

- Deliver webhooks with retries and idempotency keys.
- Sign payloads using HMAC to allow recipients to validate authenticity.

---

## OpenAPI & SDKs

- Publish OpenAPI specs for all public and partner APIs.
- Auto-generate SDKs where useful (TypeScript, Python, Dart) using the OpenAPI generator.

---

## Error Handling

- Use structured errors with codes for programmatic handling.
- Provide trace IDs for debugging across services.

---

## Backward Compatibility

- Additive changes are allowed in minor versions; breaking changes require API version bump and migration guidance.

---

Related: `ARCHITECTURE.md`, `SYSTEM_OVERVIEW.md`.
