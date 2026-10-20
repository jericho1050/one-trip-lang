# RabbitMQ outside the tick and per-seat bot jobs

Status: Accepted

## Decision

Assign bot seats through RabbitMQ. Workers connect through the ordinary player protocol. Use fenced leases, understudy fallback and asynchronous idempotent result consumers.

## Consequences

Broker failure may delay assignment/results but cannot synchronously stop ticks. Requires bounded storage and explicit degraded states; a single node is not HA.
