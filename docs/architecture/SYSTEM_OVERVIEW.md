# System Overview

This document provides a concise, developer-focused summary of the NesFlo platform and how the major components interact at a systems level. Use this page as the quick orientation before diving into more detailed architecture pages.

---

## Purpose

Provide a single-place overview that links high-level concepts (clients, API gateway, connectors, workflow engine, data stores, AI layer) with the detailed architecture documents.

---

## Quick Summary

NesFlo is a modular, API-first, event-driven platform that transforms communication and external events into structured workflows and business automation. Core properties:

- API-first: All capabilities are exposed via versioned REST APIs.
- Event-driven: Connectors produce events which flow through parsing, validation, and workflow execution pipelines.
- Modular: Parsing, workflow execution, reporting, integrations, and AI are independent services.
- Cloud-native: Designed for containerized deployment, managed databases, and object storage.

---

## Major Components

- Client Applications: Web dashboard, mobile apps, SDKs, CLI.
- API Gateway: Authentication, routing, rate limiting, versioning.
- Connector Layer: Adapters for WhatsApp, Email, Webhooks, Forms, CSV, etc., that normalize inputs into internal events.
- Parser / Message Processing Core: Normalization, template detection, extraction, enrichment.
- Workflow Engine: Orchestration, conditions, actions, scheduling, retries.
- Integration Services: Adapters to external enterprise systems (CRM, ERP, databases).
- Reporting & Analytics: Report generation, KPI computation, dashboards.
- AI Layer: Optional augmentation for classification, extraction, summarization.
- Data Stores: PostgreSQL (source-of-truth), Redis (caching, queues), Object Storage (files and reports).

---

## Typical Request Flow

1. Client or connector submits an event to `/api/v1/`.
2. API Gateway validates, authenticates, and forwards to the appropriate service.
3. Parser normalizes and extracts structured data.
4. Validation rules run; if valid, a workflow is created or an existing workflow is updated.
5. Workflow Engine executes steps, invoking connectors or integrations as needed.
6. Background workers handle long-running tasks (reports, AI jobs, imports).
7. Results are persisted in PostgreSQL and generated files placed in object storage.

---

## Operational Considerations

- Observability: Structured logs, metrics, distributed tracing across services.
- Scalability: Stateless services + horizontal scaling, queue-backed workers.
- Security: Tenant-aware multi-tenancy, RBAC, audit trails, encryption in transit and at rest.
- Resilience: Retries, dead-letter queues, manual recovery paths.

---

## Related Documents

- `ARCHITECTURE.md` — primary architecture reference.
- `WORKFLOW_ENGINE.md` — workflow execution details.
- `DATABASE.md` — database design and ownership.
- `DATA_FLOW.md` — (planned) recommended: detailed flow diagrams and examples.

---

If you'd like, I'll continue generating the other missing documentation pages in the same style (for example `DATA_FLOW.md`, `API_DESIGN.md`, `INTEGRATIONS.md`). Tell me which file to create next or I can proceed in index order.
