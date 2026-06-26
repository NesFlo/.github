# Production-Grade Architecture

This document describes the production-grade architecture for NesFlo. It is intended to capture the platform's real technical stack, service boundaries, operational requirements, and design choices needed to build a system that is more than an MVP.

## Purpose

- Define the production architecture for the current stack.
- Capture the service model, resiliency patterns, and operational expectations.
- Ensure the platform is designed for reliability, scalability, extensibility, and security from day one.

## Target Technology Stack

### Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS

### Mobile

- Flutter
- Dart

### Backend

- FastAPI
- Python 3.11+
- Pydantic for data modeling
- Uvicorn / Gunicorn for ASGI deployments

### Data & State

- PostgreSQL as the source-of-truth
- Redis for caching, queues, distributed locks, and transient state
- Object storage for file assets, reports, and export artifacts

### Infrastructure

- Vercel for frontend deployment
- Render for backend FastAPI services, workers, and background jobs
- Terraform / IaC planned for later enterprise deployments
- Docker images for portability and consistent builds

## Production-Grade Goals

NesFlo is not being designed as a throwaway prototype.
The architecture is intended to support:

- High availability
- Horizontal scaling
- Fault isolation
- Safe schema evolution
- Secure multi-tenancy
- Observability and operational maturity
- Fast feature iteration with minimal technical debt

## Service Model

NesFlo is organized into independent backend services with clear responsibilities.
Services communicate through REST APIs, events, and shared persistence patterns.

### API Gateway

Responsibilities:

- Ingress for all external traffic
- Authentication and authorization enforcement
- API versioning and request validation
- Rate limiting and quota enforcement
- Request routing to internal backend services

Production best practices:

- Keep the gateway lightweight and stateless.
- Use a managed edge or API Gateway when available.
- Emit request metrics, response times, and error rates.

### Auth Service

Responsibilities:

- User identity and session management
- JWT token issuance and validation
- API keys and service authentication
- Multi-factor authentication support planned
- Organization and role management

Production best practices:

- Keep secrets out of code and in managed secret storage.
- Use short-lived JWTs and refresh tokens.
- Store authentication events in audit logs.

### Capture Layer

Responsibilities:

- Accept inbound events from connectors and clients
- Normalize messages into a common internal event format
- Validate basic payload structure before processing
- Forward events into the pipeline

Production best practices:

- Validate input aggressively.
- Reject invalid payloads early with clear error responses.
- Use schema definitions for event normalization.

### Message Processing Core

Responsibilities:

- Parse and normalize raw communication data
- Run template detection and field extraction
- Enrich events with metadata, confidence scores, and context
- Produce validated structured records for workflows

Production best practices:

- Separate parsing from validation and workflow execution.
- Keep each parser engine small and testable.
- Capture parsing metrics and error classification.

### Validation Engine

Responsibilities:

- Apply business validation rules to structured events
- Enforce data quality, required fields, and domain constraints
- Produce validation errors or pass records onward

Production best practices:

- Support reusable rule definitions.
- Treat validation failures as first-class events.
- Use versioned rule sets for safe evolution.

### Workflow Engine

Responsibilities:

- Orchestrate actions and business logic based on events
- Evaluate conditions and decision branches
- Execute sequential, parallel, and delayed actions
- Manage workflow state and retry semantics
- Record execution history and outcomes

Production best practices:

- Store workflow state durably.
- Keep workflow execution idempotent.
- Offer observability into active and failed workflow instances.

### Integration Engine

Responsibilities:

- Communicate with external systems and SaaS platforms
- Run connectors for CRM, ERP, email, messaging, storage, and APIs
- Handle retries, backoff, and dead-letter behavior
- Keep external integrations isolated from core workflow state

Production best practices:

- Use adapter patterns to support pluggable connectors.
- Store connector configurations in secure storage.
- Respect API rate limits and circuit breaker semantics.

### Analytics & Reporting Services

Responsibilities:

- Aggregate operational metrics and KPIs
- Generate reports, dashboards, and scheduled summaries
- Support export formats and document generation

Production best practices:

- Keep analytics workloads separate from latency-sensitive APIs.
- Use batch processing for heavy report generation.
- Cache computed dashboards where feasible.

### Background Workers

Responsibilities:

- Process long-running or asynchronous tasks
- Run scheduled jobs, retries, imports, and exports
- Execute AI enrichment jobs outside request paths

Production best practices:

- Use queue-backed worker pools.
- Monitor queue depth and worker health.
- Ensure tasks are idempotent and retry-safe.

## Data Ownership & Persistence

### PostgreSQL

- Primary source of truth for core domain data.
- Store organizations, users, workflows, events, reports, audit logs, and configuration.
- Use migrations for schema evolution.
- Prefer explicit ownership boundaries in the schema.

### Redis

- Cache frequently read configuration and authorization data.
- Manage distributed locks and rate limiting.
- Support queue metadata, transient workflow state, and session data.

### Object Storage

- Persist generated reports, uploads, and export artifacts.
- Avoid storing large files in PostgreSQL.
- Reference assets by durable URLs or storage keys.

## Production Patterns

### API-First & OpenAPI

- Define all service contracts with OpenAPI.
- Use generated client SDKs for internal service interactions where appropriate.
- Keep API versions stable and support backward compatibility.

### Health Checks & Readiness

- Each service exposes health and readiness endpoints.
- Deployments should use health checks before routing traffic.
- Include dependency checks for DB, cache, and critical APIs.

### Logging & Observability

- Emit structured logs from all services.
- Capture request IDs, tenant IDs, user IDs, and workflow IDs.
- Instrument metrics for latency, throughput, errors, and queue health.
- Add distributed tracing for cross-service request paths.

### Resilience

- Use retries with exponential backoff for transient failures.
- Segment failure domains to prevent cascade failures.
- Implement dead-letter queues for unrecoverable events.
- Support manual recovery and replay for failed workflows.

### Security

- Enforce authentication on all protected endpoints.
- Apply least-privilege access controls.
- Protect secrets with a managed secrets store.
- Encrypt data in transit and at rest where possible.
- Audit all security-sensitive actions.

### Multi-tenancy

- Tenant-aware data partitioning in the database.
- Enforce tenant isolation in every service.
- Include tenant metadata in logs and events.

### CI/CD & Deployment

- Build Docker images for every backend service.
- Use GitHub Actions to run tests, linting, and build artifacts.
- Deploy frontend to Vercel and backends/workers to Render initially.
- Keep deployment configurations portable for later migration.

## Deployment Roadmap

### Stage 1 — PaaS Production

- Frontend on Vercel.
- FastAPI services on Render or comparable managed platform.
- PostgreSQL managed service (Supabase, Render Postgres, or equivalent).
- Redis managed service.
- Object storage via Supabase Storage, S3-compatible service, or cloud provider.
- Use environment variables and platform secret management.

### Stage 2 — Hardened Production

- Add monitoring, alerts, and SLOs.
- Implement backup/restore and disaster recovery procedures.
- Enable database replication and high availability.
- Define runbooks for incident response.

### Stage 3 — Enterprise-grade

- Introduce IaC (Terraform) for infrastructure, networking, and deployments.
- Move workloads to managed container platforms if needed.
- Add security controls for compliance and auditability.
- Support hybrid or private deployment models.

## Operational Priorities

- Define service-level objectives for latency, availability, and error rates.
- Monitor health at the service, workflow, and integration levels.
- Build dashboards for business operations and system reliability.
- Regularly test backups and recovery.
- Keep the architecture evolving with real usage patterns.

## Next Steps

1. Formalize service contracts and internal OpenAPI specs.
2. Define the first backend repository boundary and deployment pattern.
3. Add production-grade config, health checks, and observability to each FastAPI service.
4. Create ADRs for major architectural decisions.
5. Build the first end-to-end production flow with the API gateway, auth service, parser, validation, workflow engine, and integration engine.

## Related

- `ARCHITECTURE.md`
- `DEPLOYMENT_ARCHITECTURE.md`
- `API_DESIGN.md`
- `SYSTEM_OVERVIEW.md`
