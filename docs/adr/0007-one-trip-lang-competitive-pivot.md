# One Trip Lang competitive pivot

Status: accepted product direction by user on October 21, 2026; technical choices are the delegated recommended baseline. Supersedes Tsinelas-specific gameplay, bots, Court, fixed stations and their never-cut list for the new product. Historical documents and issues are retained as context, not active dependencies.

## Decision

Build a competitive 3D grocery trolley race. Each human owns one trolley; identical loads, 100 initial grocery points, one-time spill losses, a shared deadline and points-then-time ranking. Two-player local prototype uses WASD/arrows. Two-player online is core; four-player rooms are stretch. Player-to-player collision is disabled in the first release.

Keep meaningful engineering: shared headless simulation, authoritative outcomes, versioned replay, RabbitMQ outside the tick, bounded background simulation and licensed assets. Replace bot work/Court with a clearly labeled post-race Cargo Lab brake experiment. Add minimal IaC/K3s at the user's request, with limits and restart evidence; this supersedes the previous blanket Kubernetes exclusion. No claim of single-host high availability.

Use direct Three.js, Rapier for production and Node/WebSocket authority. The separate design prototype uses cannon-es and is not evidence of production determinism. No server rollback is required for this racing release; client prediction/reconciliation is sufficient for the initial scope, pending measured playtests.

## Consequences

The user explicitly requested a prototype now; develop that local experiment separately from competition implementation. The announced November 4 development start remains recorded, and prework eligibility still needs organizer clarification. This is not a claim of organizer permission.

Retain the repository slug and prior planning history; isolate active docs and issues under One Trip Lang. No older issue is closed as completed or silently rewritten. Read this ADR and the active plan before inheriting older requirements.
