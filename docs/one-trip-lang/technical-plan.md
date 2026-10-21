# One Trip Lang - Technical Plan

Recommended baseline, October 21, 2026. No production implementation or infrastructure exists for this plan yet.

## Build in this order

1. Reproduce the playable handling in a headless production simulation and prove the score rules.
2. Complete local two-player race and replay fixtures.
3. Run the same race through a real authority with two browser clients.
4. Add durable results, replay verification and bounded Cargo Lab jobs.
5. Package reproducible infrastructure, readable licensed assets and an offline kit.
6. Measure, tune, rehearse and freeze. Four-player support follows core gates only.

## Reuse and ownership

| Component | Choice | Work removed / responsibility |
| --- | --- | --- |
| 3D rendering | Three.js + Vite + TypeScript | Cameras, scene graph, asset loading; HTML for HUD. |
| Physics | Pinned Rapier WASM | Collision, contacts and cargo rigid bodies. Our code handles controls, legal score transitions and race rules. |
| Authority | Node.js + ws + schema validation | One process owns rooms and 60 Hz stepping. No home-grown WebSocket transport. |
| Persistence | SQLite per service | Transactional result deduplication and spool bookkeeping. Single writer ownership. |
| Messaging | RabbitMQ + amqplib | At-least-once background delivery with confirms/acks and bounded retries. |
| Verification | Vitest + Playwright | Public behavior tests and real browser flows. |
| Delivery | Docker Compose; K3s; OpenTofu/cloud-init | Local fallback, declarative process placement/limits and repeatable host provisioning. |

Pin compatible versions and lockfiles at the implementation gate; do not upgrade during demo freeze. The prototype's cannon-es dependency is a design expedient, not the production determinism guarantee.

## Runtime boundaries

Browser input -> direct WebSocket -> game authority -> snapshots/events -> browser.

Game authority -> bounded asynchronous spool writer -> outbox publisher -> RabbitMQ -> results/replay service and Cargo Lab workers.

The race step cannot await storage, HTTP, broker, LLM or an analysis result. When storage is unavailable, show results as pending and prohibit new starts after the bounded buffer fills. A running race may continue in memory; unpersisted events are not crash-durable. No claim of unlimited outage tolerance or server-crash resurrection.

Service units are coarse: game authority, results/replay API, analysis worker. Use one broker. The worker runs the same headless simulation as the authority; it does not recreate game physics. Telemetry is logs and bounded metrics, not a fourth service.

## Simulation contract

Initialize from simulation/physics version, course version, load preset and ordered player IDs. Advance one fixed tick with ordered, quantized controls. Return authoritative snapshot and emitted facts. Snapshot/restore includes engine state, heading/control filters, elapsed tick, gates, cargo ownership/lost flags, scores, finish ticks and PRNG state if introduced.

Give every grocery a stable owner and item ID. Collision masks allow environment and own cargo contacts, exclude other players. Use a simple kinematic trolley body and independent dynamic cargo; collider/render mesh separation avoids expensive triangle meshes. Precompute direction lookup values to avoid initializing gameplay with platform-dependent transcendental functions. World creation/removal order must be stable.

Spill is an irreversible state transition keyed by match/player/item. For simultaneous finish/ground-contact events: step physics, evaluate contacts and losses, evaluate gate/finish conditions, then rank. A deadline at tick N permits finishes strictly before N; do not use render time. Final delivery volume and boundary tolerance are versioned constants, displayed by debug tooling. A lost item never regains points, including on rematch unless the match ID changes.

Checkpoint acceptance requires an ordered trigger crossing or entry; finish must be directionally crossed, not trusted from a client or granted by teleport. Production recovery from leaving bounds returns the trolley to the last checkpoint, keeps lost points, and lets the clock continue; recovered intact cargo cannot gain points. On this recovery all remaining cargo is lost, with an explicit warning, so it cannot preserve a dangerous load for free. This is the production baseline; the local design preview does not implement checkpoint recovery.

## Session and network contract

Protocol messages: join, resume, lobbyState, ready, start, input, inputAck, snapshot, raceEvent, result, analysisRequest, analysisState, error. Envelopes include protocol version, match ID and server tick. Input contains session/seat ownership, monotonic sequence and bounded controls. Server owns timing and maps received input to the next admissible tick; claimed client timestamps cannot backdate scoring. Clamp rate and packet size, reject stale epochs and invalid fields, and expire stuck controls when input stops.

Initial snapshots 20 Hz; render interpolation for remote racers. Predict owned trolley/cargo, restore confirmed state and reapply unacknowledged controls when correcting. Store a bounded client input history. Do not rewind authoritative scores or impose full-world rollback. All player-facing provisional and confirmed states must be distinguished where prediction can disagree.

Room code plus session-scoped reconnect token, no account database. Token cannot take over another seat. Inactive connection sets neutral controls; after initial 10-second grace player becomes DNF. The timer never pauses online. Match continues if one competitor disconnects; remaining finisher wins under ordinary ranking. Server death aborts the match explicitly. Replays/results already committed remain available.

## Results and replay

Replay envelope records schema/sim/physics/course/load versions, initial snapshot, accepted control sequence with authoritative ticks, periodic state hashes and ordered irreversible score/finish facts. Verify against canonical state at matching ticks and report unsupported/corrupt versions. Hash comparison detects accidental mismatch; it is not cryptographic proof that a malicious server told the truth. Signatures are not required.

Persist a unique result for (match ID, rules version). Publish persistent messages using publisher confirms. Consumers transactionally write idempotency record and result before ack. Retries are bounded; poison payloads reach a dead-letter queue with an inspectable reason. Spool cap starts at 64 MiB per match as a sizing hypothesis; measure actual event volume. Test broker-only outage separately from disk or host loss.

## Cargo Lab: earned over-engineering

After finishing, choose one recorded spill. Verify the original run first. Submit an immutable job keyed by replay hash, player ID, spill ID, planner version and profile-set version. Test at most 16 predefined brake-start/duration combinations around the spill, with a maximum 10-second simulation horizon and a separate 5-second wall timeout as initial targets. Re-run from a snapshot before the intervention; keep steering and other controls fixed except the named brake edit. Label the search window and changed controls in the result.

A local avoided spill is not evidence the whole race succeeds. To claim a valid improved finish, continue the selected variant to finish/deadline under recorded remaining controls and verify it. Otherwise label only the local horizon outcome. Compare score and finish status using the same ranking rules. If no tested candidate improves the result, say so. This feature never alters the official race result.

Workers receive only versioned snapshots/inputs, not a live room handle. Duplicate delivery is normal: unique analysis key, bounded lease/attempt and transactional result commit prevent duplicate effects. Ack after persistence. Kill a worker mid-job and demonstrate redelivery. Cancellation/timeout cannot leak an unbounded simulation task.

## Deployment and budget

Start with the offered VPS if its measured resources suffice. Planning hypothesis: 4 vCPU / 8 GiB for one two-player room, broker and one capped worker. This is not a benchmark or a provider purchase recommendation. Choose a nearby region only when actual hosting is available. Do not purchase or expose new infrastructure during this planning task.

OpenTofu describes provider resources, firewall and disks; cloud-init bootstraps a pinned K3s version. For an existing provided VPS, import only resources we actually own or document the existing-host boundary. Keep provider credentials, state and kubeconfig out of Git. K3s has explicit game/worker requests and limits, readiness probes, restart policies, persistent volumes and HTTPS/WSS ingress. No public broker dashboard, database or Kubernetes API. No HA claim for one host; do not scale the game authority blindly because room ownership is stateful.

Demonstrate worker scale 1 -> 2 or restart, and measure its effect on the queued analysis workload while retaining game tick budget. If two workers overload the node, keep one and report the constraint. Kubernetes adds controlled process recovery and resource placement; it is not itself a performance result. Docker Compose uses the same images for a laptop demo with bundled assets, dependencies and sample replays. Browser runtime must not require a CDN in the release build.

## Sources checked October 21, 2026

- [Rapier determinism](https://rapier.rs/docs/user_guides/javascript/determinism/): identical versions/initialization/order are prerequisites; engine determinism does not fix nondeterministic application logic.
- [RabbitMQ reliability](https://www.rabbitmq.com/docs/reliability): client-side confirms, acknowledgement and recovery behavior are part of reliability; consumers must tolerate redelivery.
- [K3s requirements](https://docs.k3s.io/installation/requirements): platform baseline excludes application workloads, so total host sizing requires measurement.
- [OpenTofu overview](https://opentofu.org/docs/intro/): versioned infrastructure definitions and plan/apply workflow support reproducible resource management.
