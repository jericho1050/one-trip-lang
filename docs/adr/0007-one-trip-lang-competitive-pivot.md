# One Trip Lang competitive pivot

Status: accepted product direction by user on October 21, 2026; technical choices are the delegated recommended baseline. Establishes the competitive grocery-racing product. Removed product documents remain in Git history.

Historical decision, superseded in part by ADRs 0008-0009.

Update October 21: ADR 0008 supersedes the no-contact rule, kinematic handling implications, raw-ws room plumbing and isolated-player Cargo Lab assumptions below. Retained here as decision history.

## Decision

Build a competitive 3D grocery trolley race. Each human owns one trolley; identical loads, 100 initial grocery points, one-time spill losses, a shared deadline and points-then-time ranking. Two-player local prototype uses WASD/arrows. The original decision scoped two-player online with four-player rooms as stretch and disabled player-to-player collision. ADRs 0008-0009 replace both decisions: ramming and four-player online are now core.

Keep meaningful engineering: shared headless simulation, authoritative outcomes, versioned replay, RabbitMQ outside the tick, bounded background simulation and licensed assets. Use a clearly labeled post-race Cargo Lab brake experiment. Add minimal IaC/K3s at the user's request, with limits and restart evidence; this supersedes the previous blanket Kubernetes exclusion. No claim of single-host high availability.

Use direct Three.js, Rapier for production and Node/WebSocket authority. The separate design prototype uses cannon-es and is not evidence of production determinism. No server rollback is required for this racing release; client prediction/reconciliation is sufficient for the initial scope, pending measured playtests.

## Consequences

The user explicitly requested a prototype now; develop that local experiment separately from competition implementation. The announced November 4 development start remains recorded, and prework eligibility still needs organizer clarification. This is not a claim of organizer permission.

ADR 0009 supersedes the original repository and player-count decisions. Retired tasks are closed as not planned; current docs and issues define the implementation backlog.
