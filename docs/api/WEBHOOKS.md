# Webhooks

This document describes webhook subscription semantics, delivery guarantees, and security best practices.

---

## Subscription

- Clients register webhook endpoints via `POST /api/v1/webhooks` with an event filter and a secret for signing.

---

## Delivery Guarantees

- At-least-once delivery with retries and exponential backoff.
- Delivery attempts and status are recorded; failed deliveries move to a dead-letter queue.

---

## Security

- Sign payloads with HMAC using the configured secret.
- Include `X-NesFlo-Delivery-Id` and `X-NesFlo-Signature` headers for validation.
