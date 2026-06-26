# NesFlo Database Design

This document defines the core data model, storage strategy, and relationships used in the NesFlo platform.

---

## Overview

NesFlo relies on a hybrid data architecture optimized for:

- High-volume event ingestion
- Fast workflow processing
- Scalable analytics queries
- Auditability of all operations

The system is primarily built around an **event-driven data model**, where every input is stored as an immutable event and then transformed into structured workflow entities.

---

## Core Design Principles

- **Event-first architecture**: every message is an event
- **Immutability**: raw events are never modified
- **Separation of concerns**: raw data vs processed data
- **Traceability**: every structured output links back to source event
- **Scalability**: horizontal scaling for ingestion and processing layers

---

## Core Data Models

### 1. Event

Represents any incoming communication.

**Fields:**
- `id` (UUID)
- `source` (whatsapp, email, api, telegram, etc.)
- `raw_payload` (JSON / text)
- `received_at` (timestamp)
- `sender_id`
- `metadata` (device, location, headers, etc.)
- `status` (received, processed, failed)

---

### 2. Message

Normalized representation of an event.

**Fields:**
- `id`
- `event_id`
- `clean_text`
- `language`
- `entities_detected`
- `intent`
- `confidence_score`
- `created_at`

---

### 3. Workflow

Represents a structured business process derived from messages.

**Fields:**
- `id`
- `title`
- `type` (request, alert, task, report)
- `status` (pending, active, completed, failed)
- `priority`
- `created_from_message_id`
- `assigned_to`
- `created_at`
- `updated_at`

---

### 4. Workflow Step

Breaks workflows into executable steps.

**Fields:**
- `id`
- `workflow_id`
- `step_type` (action, approval, automation, notification)
- `status`
- `payload`
- `executed_at`

---

### 5. Rule Engine Table

Stores automation rules.

**Fields:**
- `id`
- `name`
- `trigger_condition`
- `action`
- `priority`
- `is_active`
- `created_at`

---

### 6. Connector Logs

Tracks external integrations.

**Fields:**
- `id`
- `connector_type`
- `request_payload`
- `response_payload`
- `status`
- `timestamp`

---

## Data Flow

1. Incoming message arrives → stored as **Event**
2. Event is normalized → **Message**
3. NLP processes Message → intent + entities extracted
4. Message generates → **Workflow**
5. Workflow executed via **Workflow Steps**
6. Automation rules evaluated via Rule Engine
7. External systems triggered via Connectors

---

## Storage Strategy

### Primary Database
- PostgreSQL (structured data)
- Used for workflows, users, rules, connectors

### Event Store
- Scalable log-based storage (e.g. Kafka + persistence layer)
- Stores raw events

### Cache Layer
- Redis
- Used for:
  - Active workflows
  - Rule evaluation caching
  - Session data

### Analytics Store (Optional)
- ClickHouse / BigQuery
- Used for:
  - Reporting
  - Aggregations
  - Dashboards

---

## Indexing Strategy

- Index `event.source`
- Index `message.intent`
- Index `workflow.status`
- Composite index on `(created_at, type)`
- Full-text search on `clean_text`

---

## Scalability Considerations

- Partition events by time (daily/weekly)
- Separate ingestion and processing services
- Async processing for NLP pipeline
- Use queue-based workers for workflow generation

---

## Security Considerations

- Encrypt sensitive payload fields
- Role-based access control (RBAC)
- Audit logs for all workflow changes
- API authentication required for external access

---

## Future Enhancements

- Multi-region database replication
- Real-time streaming analytics
- Graph database for relationship mapping
- AI-driven schema optimization