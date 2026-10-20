# Shared simulation and authoritative networking

Status: Accepted

## Decision

Use pinned Rapier WASM plus custom slipper forces inside a deterministic headless core. Authority sends snapshots with bounded rollback; clients predict and reconcile.

## Consequences

Avoids building collision physics and makes one implementation serve bots, replay and Court. Determinism still requires our own fixed ordering, PRNG and cross-runtime checks.
