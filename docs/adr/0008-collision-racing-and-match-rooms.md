# Shared-track collisions and isolated match rooms

Status: accepted October 21, 2026. The user approved the revised wobbling/ramming prototype and requested the PR, epic, tasks, assets and infrastructure plan. Technical selections follow the user's delegated recommendations. Supersedes ADR 0007's no-contact rule and affected networking/analysis assumptions.

## Decision

Ramming and physical cargo wobble are core gameplay. Two humans occupy separate start slots on the same course, each with their own trolley, groceries, camera and controls. Contacts may disturb both loads. Only an actual cargo-loss rule deducts points; ownership never changes. Finish/DNF removes the racer and cargo from active collisions after recording the outcome. Four-player matches remain stretch.

Use a dynamic Rapier chassis with arcade drive forces, simple vertical support and damped pitch/roll. Do not lock the deck flat or build a full vehicle simulator. Reproduce the approved local prototype's observable behavior through production tests; do not copy cannon-es coefficients and claim equivalence.

Use Colyseus on Node for room/seat/reconnect lifecycle and WebSocket transport, replacing the planned raw-ws room plumbing. Keep the shared headless simulation behind a narrow room adapter. Physics snapshots, accepted input ticks and score events remain explicit. Each room owns a separate world and match history. One bounded server process may host multiple rooms; a room is not a VPS or a Kubernetes pod. Single process means no Redis/distributed matchmaker in v1.

Whole-world interactions require whole-world reconciliation and replay. Client predictions remain provisional. Cargo Lab restores all players, changes only the selected brake input and keeps opponents' recorded controls fixed. It must disclose this counterfactual assumption and never claim to predict a human's response.

## Why

The creator preferred the shared-track collision experience. The first collision revision was too stable because its deck could not pitch/roll and its load was squat. The corrected preview passed idle, careful-drive and impact regressions and was accepted for the product direction. This evidence does not establish production determinism, online feel or hosting capacity.

Colyseus removes routine room lifecycle work. Rapier supplies rigid-body collision. Our engineering remains in the shared race rules, collision-aware synchronization, replay verification, bounded experiments and recoverable background work. RabbitMQ stays outside the tick. K3s/IaC earns its scope through reproducible deployment, resource limits and worker recovery.

## Consequences and gates

- New collision/wobble and multi-room-isolation tasks become required before online/release completion.
- Ported behavior must pass idle retention, careful finish, visible side-swipe, hard spill, immutable ownership and finisher clearing scenarios.
- Start with one admitted public match; test two concurrent matches before increasing the configured limit. This is a conservative policy, not measured maximum capacity.
- Preserve proposal/prework eligibility records and the November 4 production start. This PR is planning and does not assert organizer approval.
- Use the offered VPS when suitable; paid fallback is described in the infrastructure plan. No resources are provisioned by this decision.

References: [Colyseus rooms](https://docs.colyseus.io/room), [room ownership](https://docs.colyseus.io/scalability), [Rapier determinism](https://rapier.rs/docs/user_guides/javascript/determinism/). Documentation checked October 21, 2026; pin and verify actual dependency versions at implementation.
