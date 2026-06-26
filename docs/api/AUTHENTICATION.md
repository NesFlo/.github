# Authentication

This document outlines authentication mechanisms for NesFlo APIs and services.

---

## Methods

- JWT Bearer tokens for user sessions and short-lived service sessions.
- API Keys for service-to-service calls; scope-limited and tenant-aware.
- OAuth2 support as an extension for third-party integrations.

---

## Token Usage

- Provide tokens via `Authorization: Bearer <token>` header.
- Validate token audience, issuer, expiry, and scopes at the gateway.
