# Security Architecture

This document summarizes the security controls and architecture decisions for NesFlo. It is intended for architects, implementers, and operators.

---

## Core Principles

- Defense in depth
- Least privilege
- Secure by default
- Auditability and traceability

---

## Authentication & Identity

- Primary auth: JWT tokens issued by Authentication Service.
- Support for API keys for machine-to-machine calls.
- OAuth2 integration for third-party delegated access.

---

## Authorization

- Role-based access control (RBAC) scoped to tenant and workspace.
- Fine-grained permissions for critical actions (reporting, integrations, admin).

---

## Data Protection

- Encryption in transit: TLS for all external/internal communication.
- Encryption at rest for databases and object storage.
- Secrets management using a centralized secret store.

---

## Multi-Tenancy Isolation

- Logical separation by tenant ID in application and data access layers.
- Tenant-aware queries and strict permission checks at service boundaries.

---

## Network & Infrastructure

- Use network segmentation and security groups for service isolation.
- Allow-list management for administrative access.

---

## Audit & Logging

- Immutable audit logs for security-relevant events.
- Retention policies and secure storage for audit data.

---

## Incident Response

- Define incident response playbooks for authentication failures, data exfiltration, and service compromise.
- Alerting and runbooks for operators.

---

## Compliance & Hardening

- Dependency vulnerability scanning.
- Regular penetration testing and security reviews.

---

Related: `ARCHITECTURE.md`, `SYSTEM_OVERVIEW.md`, `SECURITY_ARCHITECTURE.md`.
