# Technical implementation plan

Planning baseline, not an implementation report. All numerical budgets below are initial targets to validate.

## Architecture and ownership

Browser rendering and HUD -> direct WebSocket -> authoritative game server. Bot workers also connect through that public gameplay protocol. The server alone owns hit, phase and score decisions. Every finalized squash increments one shared team score; seat attribution is evidence, not individual hit ranking. Humans and bots cooperate; bots choose legal throws to help squash the target, with no sabotage behavior or separate victory condition.

Outside the tick: bot seat requests -> RabbitMQ -> workers; finalized facts -> asynchronous outbox publisher -> RabbitMQ -> results/replay and telemetry consumers. No broker, database or remote model wait can appear in a simulation step.

Planned code units: client application; game server; bot worker; results/replay service; shared simulation, protocol, replay and asset-manifest packages. Keep these in one pnpm monorepo with one lockfile. The initial repo is documentation only.

The shared simulation has a small interface: initialize from a versioned fixture, advance one tick with ordered inputs, capture/restore a snapshot and return canonical hash data. The Court module accepts a replay plus an intervention and returns two verified trajectories and a verdict with assumptions. The publisher accepts finalized event batches without making tick execution await them.

## Simulation and reproducibility

Use pinned Rapier WASM plus deterministic custom forces. Fixed 1/60-second steps, quantized player controls, stable creation/order/IDs, seeded PRNG streams and no wall clock or I/O in the core. Avoid platform-dependent transcendental operations in simulation logic; use committed lookup tables where necessary. Rendering may interpolate freely without influencing physics.

Snapshot all gameplay state, PRNG counters, cooldowns, physics state and cockroach state. Hash canonical ordered state, excluding timestamps, sockets, UI and telemetry. Compare hashes only at the same tick/version after authoritative inputs have arrived. Prediction divergence is normal; persistent authoritative disagreement is an error.

Baseline replay verifies recorded player and cockroach inputs. A separate brain reproducibility fixture checks that deterministic decisions agree with the recorded log. Cross-browser save/restore and 10,000-tick tests are required before dependent features rely on reproducibility.

## Network contract and finalization

Versioned messages: join, resume, ready, input, input acknowledgement, snapshot, phase, ballot, reveal and error. Each player input includes match ID, seat/session ownership, sequence number, bounded target tick and quantized control values. Validate every field; reject stale epochs and duplicate sequences idempotently. Do not trust client-supplied hits, scores or roles.

Initial tick rate 60 Hz, snapshot rate 20 Hz, maximum rollback eight ticks. The server retains bounded snapshots and accepted inputs. Within-window inputs can revise provisional state; older ticks are finalized. Late inputs receive an explicit rejection. Predicted HUD outcomes remain provisional until confirmed. An injected 250 ms delay exceeds an eight-tick window; do not promise rollback hides it. Demonstrate within-window recovery separately from Court's delay experiment.

Use an authoritative scheduled release tick for controlled throws. Latency Lab records the intended release tick, chosen added delay and actual admission. The Court fixture must start with enough lead time and an intervention range that the factual throw is accepted; reject experiments whose factual baseline cannot be verified.

Reconnect grace initial target 15 seconds. Restore the same human seat using a session token. No human-to-bot replacement during a bout; absent humans idle and missed ballots abstain. Role metadata and operator controls use a separate authenticated channel and must never appear in participant snapshots, public replay metadata or room lists before reveal.

## Cockroach and slipper model

Start with collision bodies, gravity, drag and constrained orientation/spin. The air signal depends on speed, effective facing area, direction and bounded inverse-distance falloff. Clamp near-field values to avoid singularities. Cockroach trigger thresholds, reaction delays and escape angles must be sourced and documented before being described with exact biological numbers. The handoff's numerical spikes are unverified claims, not benchmarks.

Use a seeded deterministic escape policy. Regression fixtures compare face-on and edge-on approaches under fixed conditions; they demonstrate the model, not universal real-world behavior. Display signal magnitude, threshold crossing and reaction on a replay overlay. Avoid CFD and sophisticated tumbling until the core works.

## Bots and RabbitMQ seat lifecycle

Lobby emits a durable per-seat job containing match, seat, lease epoch and a short-lived token, never an identity payload visible to players. Worker claims and connects like any client. Authority fences ownership: only the current epoch can submit inputs. Acknowledge the assignment once the authority confirms seating; worker health/replacement is managed by the seat lease, not a permanently unacknowledged queue delivery.

After a five-second unclaimed-seat deadline, create an understudy client under a new fenced epoch. Detect worker loss by heartbeat and issue a new epoch for a replacement bot only. Duplicate and late workers cannot take over an occupied epoch. Keep fallback computation off the tick execution context, even if hosted in the same process group.

A planner sees only public snapshots and estimates possible futures; it cannot read the authority's seed or future cockroach decisions. Candidate count is the difficulty unit, with a separate hard deadline. Count simulated flights directly. On timeout choose a valid fallback input. Use bounded reaction delay and smooth aim variation first; advanced human motor models are optional.

## Events, buffering and recovery

Every finalized event includes event ID, match ID, finalized tick, simulation version, sequence and payload. Persist an outbox through a bounded worker boundary; publish with confirms asynchronously and acknowledge consumers only after their transaction commits. Unique event IDs make scores and replay batches duplicate-safe. Use bounded telemetry queues with explicit drops and dead-letter/retry limits for durable consumers.

Distinguish outcomes: local in-memory provisional, durable finalized, and externally published. The HUD says pending until a required durable write succeeds. Never claim data survives a server crash before it is persisted; crash recovery is stretch.

Initial spool cap 64 MiB per active match; validate with measured event sizes. A broker outage alone should fit at least the 60-second acceptance fixture. If storage is full or unavailable, expose degraded/pending status, preserve what is already durable and prevent the next bout from starting. Do not silently discard durable facts, wait inside a tick, or promise unlimited outage tolerance.

Single-node RabbitMQ with durable queues and persistent volume; no HA claim. One-node quorum queues do not make the host failure-tolerant. Independent consumers for results/replay and telemetry; no separate lobby database service unless needed.

## Replay format and Slipper Court

Court is a separate evidence view that players may open after a miss, not a prerequisite for cooperative play or the bot-guessing reveal. It remains a planned core demonstration feature. The complaint button means "Did our deliberately added network delay cause this miss?"; it does not accuse a teammate or bot.

Replay envelope: format/simulation/physics version, match settings, initial snapshot, ordered accepted inputs, recorded cockroach decisions, seed data for authorized post-bout analysis, periodic hashes, finalized events and injected-delay metadata. Keep participant replay access restricted until reveal. Compress only after correctness. Do not promise the handoff's 200 KB size.

Baseline Court branch must reproduce the factual replay. For an eligible controlled complaint, change only the intentional delay applied to the claimant's recorded control stream. Use the same pre-intervention snapshot and random streams; hold other players' recorded controls fixed. Re-run cockroach sensing/decisions because its reaction to the changed air field is an outcome, not a fixed fact. Any later physical divergence is a consequence of the intervention. Tick/actor-keyed random draws avoid incidental PRNG call-order drift.

Use a fixed three-second analysis horizon from intended release, with stable claimant projectile identity. Factual miss plus alternate hit supports the excuse within this experiment; factual miss plus alternate miss rejects it. Missing delay metadata, invalid baseline, unsupported version or invalid timing yields inconclusive. A factual hit means there is no miss to contest.

Show both trajectories, timestamps, added delay, outcomes and the assumption that other players did not adapt. Never change official points. This is conditional simulation evidence, not proof of what humans or an actual insect would have done. Optional LLM text can paraphrase structured evidence only; templates are the offline default.

## Hosting, asset delivery and security

One nearby VPS running Compose. Confirm provided VPS resources before choosing paid hosting. Start with 2 vCPU/4 GiB as a sizing hypothesis, not a guarantee; profile before renting more. Use HTTPS/WSS for remote play, restricted management access and no public RabbitMQ dashboard. Secrets in environment files excluded from Git. Bound message size, action rate, room count and session lifetime.

Preload images, dependencies, models, audio and fixtures on primary and spare demo machines. No runtime CDN, external font or model dependency. Use real browser audio-unlock interaction and provide mute. Keep visual meshes independent from simple collision proxies. Host all licensed runtime assets locally.

## Validation and delivery order

1. Minimal throw and replay restore across supported runtimes.
2. Authoritative scored throw with a durable event; two clients agree.
3. Bounded rollback/reconnect and role-safe messages.
4. Air-sensing model and visible comparison.
5. Planner, per-seat queue lifecycle, spotting and reveal.
6. Broker-outage recovery and standalone replay verification.
7. Controlled Court comparison and honest UI.
8. Offline packaging, performance checks and three rehearsals.

Implement through the issue dependency graph. Some independent slices may overlap; dates do not override prerequisites. Rule/source research and documentation can happen before November 4; application implementation cannot without permission.

## References checked during planning

- Rapier determinism: https://rapier.rs/docs/user_guides/javascript/determinism/
- React Three Fiber: https://r3f.docs.pmnd.rs/tutorials/how-it-works
- Kenney licensing: https://kenney.nl/support

Library versions must be pinned and compatibility verified when development starts. These references do not validate any unmeasured performance claim.
