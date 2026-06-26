# REST API Reference

This document summarizes the primary REST resources and sample request/response shapes used by NesFlo.

---

## Resource Examples

- `POST /api/v1/events` — submit a canonical event or connector payload.
- `GET /api/v1/workflows` — list workflows (supports filtering and pagination).
- `POST /api/v1/workflows/{id}/actions` — trigger an action on a workflow.
- `GET /api/v1/reports/{id}` — download a generated report.

---

## Error Model

Responses use the following error body:

```json
{
  "code": "ERR_CODE",
  "message": "Human readable message",
  "details": { }
}
```

---

## Idempotency

- Clients should provide `Idempotency-Key` headers for operations that must be safely retried.
