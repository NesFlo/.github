# NesFlo Workflow Engine

This document defines how NesFlo transforms structured messages into executable business workflows.

---

## Overview

The Workflow Engine is the core execution layer of NesFlo. It is responsible for:

- Creating workflows from structured messages
- Managing workflow lifecycle
- Executing workflow steps
- Coordinating automation rules
- Tracking execution state and history

It sits between the **AI parsing layer** and the **execution/integration layer**.

---

## Core Responsibilities

- Workflow creation from parsed messages
- Step decomposition and orchestration
- Execution scheduling
- State management
- Failure recovery and retries
- Integration with rule engine and connectors

---

## Workflow Lifecycle

### 1. Creation
A workflow is created when:
- A message is classified as actionable
- A rule triggers workflow generation
- A manual user action creates a workflow

---

### 2. Initialization
- Assign workflow type
- Set priority level
- Attach source message ID
- Generate initial steps

---

### 3. Execution
- Steps are executed sequentially or in parallel
- Each step updates workflow state
- External services are called via connectors

---

### 4. Monitoring
- Track progress in real-time
- Log execution results
- Capture errors and retries

---

### 5. Completion
- Mark workflow as completed
- Archive execution logs
- Trigger downstream actions (reports, notifications)

---

## Workflow Types

### 1. Request Workflow
Used for incoming user or system requests.

Example:
- “Request fuel delivery”
- “Generate report”

---

### 2. Automation Workflow
Triggered by rules.

Example:
- Low inventory → trigger reorder
- New message → auto-response

---

### 3. Alert Workflow
Used for critical notifications.

Example:
- System failure alert
- Threshold breach

---

### 4. Reporting Workflow
Generates scheduled or on-demand reports.

---

## Workflow Structure

### Workflow Object

- `id`
- `type`
- `status`
- `priority`
- `source_message_id`
- `created_at`
- `updated_at`

---

### Step Object

Each workflow consists of steps:

- `id`
- `workflow_id`
- `order_index`
- `step_type`
- `action`
- `status`
- `input_payload`
- `output_payload`
- `retry_count`

---

## Execution Model

### Sequential Execution
Steps run one after another.

Used for:
- Approval flows
- Dependent tasks

---

### Parallel Execution
Steps run simultaneously.

Used for:
- Notifications
- Multi-system updates

---

### Conditional Execution
Steps executed based on conditions.

Example:
- If approval = true → continue
- Else → cancel workflow

---

## State Management

Workflow states:

- `pending`
- `active`
- `waiting`
- `failed`
- `completed`
- `cancelled`

State transitions are strictly controlled to ensure consistency.

---

## Error Handling

- Automatic retries with exponential backoff
- Dead-letter queue for failed steps
- Manual intervention triggers
- Partial workflow rollback support

---

## Integration with Rule Engine

- Rules can create workflows
- Rules can modify workflow steps
- Rules can cancel workflows
- Priority rules override default behavior

---

## Integration with Connectors

Workflow steps can trigger external systems:

- APIs
- Email services
- Messaging platforms
- ERP/CRM systems

All connector responses are logged for traceability.

---

## Performance Considerations

- Asynchronous step execution
- Queue-based orchestration
- Stateless execution workers
- Horizontal scaling support

---

## Observability

- Workflow execution logs
- Step-level tracing
- Metrics:
  - Completion time
  - Failure rate
  - Retry count
- Distributed tracing support

---

## Security

- Authorization checks before execution
- Step-level permission control
- Audit trail for all actions
- Encrypted payload transmission

---

## Future Improvements

- AI-driven workflow optimization
- Self-healing workflows
- Predictive step failure detection
- Visual workflow builder UI