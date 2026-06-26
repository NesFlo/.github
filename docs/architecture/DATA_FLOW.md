# Data Flow

This document describes the event and data processing pipelines used across NesFlo. It complements `ARCHITECTURE.md` and `SYSTEM_OVERVIEW.md` with concrete flow diagrams, typical payload shapes, and failure-handling patterns.

---

## Goals

- Provide clear, reproducible paths for data as it moves from connectors to persistent storage.
- Describe normalization, validation, transformation, and routing steps.
- Outline retry, dead-letter, and manual review strategies.

---

## End-to-end Flow (Overview)

```text
Connector -> API Gateway -> Parser -> Validation -> Transformation -> Workflow Engine -> Integrations/Storage
```

Key points:

- Connectors convert channel-specific payloads into a canonical event format.
- The Parser extracts fields, detects templates, and attaches metadata (confidence, source, timestamps).
- Validation enforces business rules and schema expectations.
- Transformation maps fields to internal domain models usable by workflows.
- The Workflow Engine coordinates actions and may emit new events.

---

## Canonical Event Shape

Example JSON (simplified):

```json
{
  "event_id": "uuid",
  "tenant_id": "org_123",
  "source": "whatsapp",
  "received_at": "2026-06-26T12:34:56Z",
  "raw": { /* raw connector payload */ },
  "parsed": {
    "type": "fuel_request",
    "fields": {
      "location": "Site A",
      "quantity": 500,
      "unit": "liters"
    },
    "confidence": 0.93
  },
  "status": "parsed"
}
```

---

## Validation and Enrichment

- Validation: Schema checks, required fields, business rule checks (e.g., allowed quantities).
- Enrichment: Geo lookups, user directory resolution, pricing lookup, historical context.
- On validation failure: mark event `validation_failed` and route to manual review queue with reason codes.

---

## Transformation and Routing

- Transformation converts `parsed.fields` into domain models (e.g., `Order`, `Inspection`, `Report`).
- Routing selects the appropriate workflow based on `type`, tenant rules, and priority.

---

## Reliability Patterns

- Retry with exponential backoff for transient downstream failures.
- Dead-letter queue for unprocessable events after N retries.
- Manual review queue with human-in-the-loop corrections.
- Event immutability: do not mutate historical events; provide compensating events to represent state transitions.

---

## Observability

- Trace events with request IDs across services.
- Emit structured logs with `event_id`, `tenant_id`, `workflow_id`.
- Metrics: parse success rate, validation failure rate, average processing latency.

---

## Examples

- WhatsApp message -> fuel request -> create `Order` record -> notify operations.
- CSV upload -> batch parse -> multiple `events` -> bulk workflows -> generate summary report.

---

Related: `SYSTEM_OVERVIEW.md`, `ARCHITECTURE.md`, `WORKFLOW_ENGINE.md`.
