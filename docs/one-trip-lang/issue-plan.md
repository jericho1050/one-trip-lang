# One Trip Lang - Epic and Implementation Breakdown

Current baseline: ADR 0008. Each leaf has one observable acceptance scenario. AFK is specified work; HITL needs human action/review. Production start follows the recorded November 4/eligibility gate.

## Epic

Deliver the approved shared-track collision race, authoritative private rooms, whole-match replay, bounded Cargo Lab, licensed assets, reproducible infrastructure and offline release. Two players core, four stretch. All core evidence gates must pass; planning completion is not implementation completion.

## T0: Proposal, rules and asset readiness

Milestone: OTL M0 - Proposal and product baseline. Make the new competitive product and submission status concrete before production implementation.

### P1: Refresh the proposal for the competitive grocery race

HITL | core | Due 2026-10-21 | Blocked by: none

Use the official proposal headings, keep team identity placeholders where unknown, and describe the current game and earned engineering. Record submission separately; do not submit without instruction. Include shared-track ramming, individual POVs and whole-match replay. Use ADR 0008 as the current scope.

Acceptance: Given the current PRD, the owner can review a concise official-template proposal describing competitive trolleys, cargo points, deadline, replay and background analysis, with submission status explicitly recorded.

Implementation steps:
- Replace the Tsinelas premise and demo claims.
- Check every claimed feature is implemented or clearly planned.
- Preserve official structure and record owner review/submission status.

### P2: Record development eligibility and the production start gate

HITL | core | Due 2026-10-21 | Blocked by: none

Record the announcement, November 4 start and status of organizer clarification on local prework. Distinguish user authorization from competition eligibility.

Acceptance: Given the event instructions, a dated rules record identifies permitted prework, unresolved organizer questions and the condition/date that permits production implementation without asserting unreceived approval.

Implementation steps:
- Record the supplied event dates.
- Track the local prototype as pre-development work.
- Record organizer answer when available, or mark eligibility unresolved.

### P3: Select the minimum licensed grocery and environment assets

AFK | core | Due 2026-11-07 | Blocked by: none

Inspect the verified Kenney Food Kit, City Kit Suburban and Impact Sounds shortlist in docs/one-trip-lang/assets.md. Select only the minimum needed files; use original primitives for missing trolley/packaging. Produce source/license/checksum manifest and a readable six-grocery reference sheet. No purchase required.

Acceptance: Given the asset shortlist, every selected file has a source URL, license and required attribution, and a small reference sheet shows the six groceries can be distinguished.

Implementation steps:
- Inspect actual pack files; do not assume the shortlist contains every grocery.
- Record per-file source, author, license, checksum, modifications and attribution.
- Use simple independent collider proxies and document primitive fallbacks.

## T1: Complete a fair local grocery race

Milestone: OTL M1 - Playable local race. Deliver the two-human local collision race with visible wobble, fair cargo losses, deadline, result and rematch.

### S1: Drive one trolley through the production course

AFK | core | Due 2026-11-07 | Blocked by: P2

Create the pinned production simulation and browser view with acceleration, braking/reverse, one bump, ordered corner gates and the finish. Reuse libraries; isolate authoritative stepping from rendering. Use a dynamic chassis with arcade drive, vertical support and damped pitch/roll; keep physical body state separate from render smoothing.

Acceptance: Given a fresh local run, a recorded control sequence drives the trolley through both gates to the finish, while the same sequence at different render rates reaches the same authoritative tick/state.

Implementation steps:
- Pin runtime and physics dependencies.
- Create headless initialization/step/snapshot interfaces.
- Connect input and follow camera to the visible route.

### S2: Complete the cargo score and deadline loop

AFK | core | Due 2026-11-07 | Blocked by: S1

Add six physical groceries, named one-time loss events, authoritative deadline, finish delivery-volume check and points/time ranking.

Acceptance: Given a fixture with a wobble, repeated ground contact, an off-cart finish item and two finishers, the score ledger deducts only genuine losses once and ranks by points then finish tick; a race reaching the exact deadline becomes DNF.

Implementation steps:
- Create stable owned cargo and collision masks.
- Implement irreversible loss and finish/deadline transitions.
- Show the ledger, timer and result with rule fixtures.

### C1: Ram a rival with physical wobble and fair cargo losses

AFK | core | Due 2026-11-07 | Blocked by: S2

Port the approved feel to Rapier: dynamic chassis, low bumper, physical pitch/roll with damped recovery and independent cargo. Contacts affect both loads; cargo ownership never changes. Clear finished/DNF racer bodies. No cosmetic wobble substitute or arbitrary contact penalty.

Acceptance: Given a versioned test course and control fixture suite, idle for 45 seconds retains 100 points, careful driving finishes with at least 80, a side-swipe visibly tilts cargo (initial target 8 degrees), a hard crash spills without pass-through, each lost item penalizes its original owner once, and a cleared finisher cannot block the remaining racer.

Implementation steps:
- Use a shared world and deterministic body creation/removal ordering.
- Tune chassis support, pitch/roll damping, cargo proportions and sleep/wake through the idle/careful/impact scenarios.
- Show impact/loss feedback in the playable browser and capture a short replay plus assertions.

### S3: Play and rematch with independent local controls

AFK | core | Due 2026-11-07 | Blocked by: C1

Add split-screen simultaneous WASD/arrows, identical load presets, common countdown, global local pause and clean rematch.

Acceptance: Given two local players holding different controls concurrently, both trolleys respond independently; after finish/deadline a rematch restores both to 100 points, identical loads, zero elapsed race time and no held input.

Implementation steps:
- Wire two input streams without shared bindings.
- Render independent cameras and readable colliding rivals.
- Reset all state and handle focus-loss pause; clear finished/DNF bodies from collisions.

## T2: Race a friend in an authoritative online room

Milestone: OTL M2 - Two-player online race. Deliver authoritative online collision races with individual POVs, reconnects and isolated private rooms on one bounded server.

### S4: Join and finish a real two-browser race

AFK | core | Due 2026-11-12 | Blocked by: S3

Use Colyseus room/seat lifecycle and direct WebSocket transport with a versioned race adapter. Implement room code, ownership, ready/countdown, authoritative collision snapshots, individual online POVs and result/rematch.

Acceptance: Given two independent browsers in one room, they ready, collide, spill cargo and rematch with identical authoritative loss events, deadline and ranking; a third join and a client-sent score are rejected.

Implementation steps:
- Pin Colyseus and define a validated room adapter around the shared simulation.
- Keep one world per room and enforce seat ownership, new match IDs and input epochs.
- Show the complete lobby-to-rematch flow and each player’s own follow camera.

### R1: Run isolated private matches on one bounded server

AFK | core | Due 2026-11-12 | Blocked by: S4

Host separate Colyseus rooms with separate physics worlds, clocks, seats, input epochs and result/replay records. Add configurable admission limit, empty-room TTL and clear busy/full responses. No Redis, sharding or per-match pod controller.

Acceptance: Given four browsers in two private two-seat rooms, a collision, rematch or disposal in room A cannot change room B; cross-room tokens and a third seat are rejected, and attempting an additional room at the configured cap returns busy while both active races continue.

Implementation steps:
- Scope all mutable simulation/session data to the room and each rematch to a new match ID.
- Exercise two rooms in staging and dispose idle rooms without touching another world.
- Expose cap/active-room counts and reject excess admissions; public cap stays one until load evidence permits more.

### S5: Keep racing responsive under delay and hostile input

AFK | core | Due 2026-11-12 | Blocked by: S4

Predict/reconcile the small full interacting world, including rivals and cargo, from complete authoritative snapshots. Bound remote-input extrapolation and local input history; validate size/rate, seat/room ownership, sequence and expiry. No server rollback.

Acceptance: Given a head-on collision at 150 ms RTT and 30 ms jitter plus duplicate, stale and forged-seat inputs, both browsers converge on the same authoritative cargo losses and ranking, no unauthorized input changes another seat, and silence cannot leave throttle stuck.

Implementation steps:
- Restore complete world snapshots and reapply pending local controls with bounded remote-control extrapolation.
- Keep provisional motion separate from server-confirmed loss/finish events.
- Record collision correction magnitude, tick timings and abuse rejection on the reference build.

### S6: Reconnect a seat without pausing the race

AFK | core | Due 2026-11-12 | Blocked by: S4

Neutralize stale input on disconnect, reclaim the same seat with its token within grace, and mark DNF after grace while rivals keep racing. Remove expired DNF trolley/cargo from the collision world; preserve its immutable result.

Acceptance: Given a dropped connection, resuming within 10 seconds restores the same seat and current clock; a second drop beyond grace produces DNF and clears that racer’s collision bodies without stopping the rival or allowing another token to steal the seat.

Implementation steps:
- Implement bounded grace and seat token validation.
- Show reconnecting/expired states.
- Test the race clock and stale-control behavior during loss.

## T3: Verify races and test useful braking alternatives

Milestone: OTL M3 - Evidence and useful analysis. Show truthful replay and bounded Cargo Lab output that survives background-service failures.

### S7: Verify a recorded race against the shared simulation

AFK | core | Due 2026-11-07 | Blocked by: C1

Record versioned initial state, admitted controls, irreversible facts and canonical hashes; restore and verify with a readable replay view.

Acceptance: Given a pinned 10,000-tick whole-match fixture containing ramming, spills and finisher clearing, Node and supported Chromium replay identical state hashes and score events; altered input or unsupported versions produce a visible verification failure.

Implementation steps:
- Record complete world/controller state, admitted controls for all racers and ordered outcome/removal events.
- Implement version-checked baseline verification and replay seeking.
- Capture runtime/build evidence; do not reuse cannon-es results as Rapier proof.

### S8: Publish durable results and replay work outside the tick

AFK | core | Due 2026-11-18 | Blocked by: S4, S7

Create the bounded spool/outbox and RabbitMQ publisher with separate results/replay consumer; unique keys make redelivery harmless.

Acceptance: Given a 60-second broker interruption while a race completes, play continues and shows pending persistence/publication accurately; after recovery exactly one effective result and replay record exists for the match.

Implementation steps:
- Use a dedicated spool writer thread/process, bounded handoff and honest pending/backpressure states.
- Use persistent messages, publisher confirms and post-commit acknowledgements.
- Exercise broker outage, duplicate delivery and disk-full admission refusal.

### S9: Run a bounded earlier-braking Cargo Lab experiment

AFK | core | Due 2026-11-18 | Blocked by: S7, S8

From a verified whole-match replay, queue at most 16 brake variants around one spill. Resimulate all colliding bodies while holding opponents’ recorded controls fixed, and label that assumption. Continue a candidate to deadline before claiming a better finish.

Acceptance: Given a collision replay with a known improvable variant and a non-improvable fixture, the UI verifies the factual baseline and shows changed controls plus the fixed-opponent-input assumption, then reports a verified tested outcome or no improvement without changing official race points.

Implementation steps:
- Define an immutable analysis key and bounded profile/horizon/timeout budgets.
- Restore and resimulate the entire world, including rival cargo and body removals.
- Label hypothetical opponent behavior and verify full completion before claiming a better finish.

### S10: Recover analysis jobs without duplicate effects

AFK | core | Due 2026-11-18 | Blocked by: S8, S9

Make worker termination, poison data, retry exhaustion and concurrent duplicate jobs observable and bounded.

Acceptance: Given a worker killed mid-analysis and duplicate redelivery, a replacement produces one committed analysis for the same key; invalid data reaches a bounded terminal failure and the live race continues.

Implementation steps:
- Fence attempts or use transactional unique result keys.
- Ack after durable completion and bound retries.
- Expose pending, failed and retryable states without hiding races.

## T4: Host a readable game with repeatable infrastructure

Milestone: OTL M4 - Hosted and recognizable. Combine licensed art and clear HUD with reproducible hosting and protected game resources.

### S11: Make the race readable with licensed assets and cues

AFK | core | Due 2026-11-23 | Blocked by: S3, P3

Replace essential grayboxes with sourced low-poly grocery/road/trolley visuals, readable player IDs, camera framing, sound/mute and credits. Keep collider behavior unchanged.

Acceptance: Given a desktop browser on the agreed minimum viewport, a new player can identify all six grocery types, their own trolley, the next gate, a named score loss and final result without clipped HUD; mute and credits work.

Implementation steps:
- Import selected optimized assets with per-file manifest and primitive fallbacks.
- Add start, impact, loss and finish cues with mute and credits.
- Check both colliding carts, individual cameras, named penalties and result readability.

### S12: Deploy one reproducible HTTPS race environment

AFK | core | Due 2026-11-23 | Blocked by: S4, S8, P2

Implement docs/one-trip-lang/infrastructure.md: offered VPS or paid Lightsail fallback, OpenTofu/cloud-init, one-host K3s, HTTPS/WSS, persistent storage, restricted management, CI images and off-host backups. Account/region/DNS/credentials must be available before apply.

Acceptance: Given a clean authorized host, pinned provisioning/deployment creates a working two-browser collision race and background result pipeline, and a backup restores a committed result/replay into a replacement test environment using the documented runbook.

Implementation steps:
- Resolve host/account/region/DNS, budget alerts and provided-host versus managed-resource boundaries.
- Build immutable images; declare ingress, probes, secrets references, resource caps and persistent volumes.
- Run clean install, room drain/rollback, backup/restore and cost-aware teardown; record evidence.

### S13: Protect live race resources while workers restart or scale

AFK | core | Due 2026-11-23 | Blocked by: S9, S10, S12

Set explicit worker budgets and K3s resource limits; demonstrate one-worker recovery and evaluate a second worker without duplicating game authority.

Acceptance: Given an active reference race and queued analysis jobs, restarting a worker recovers work without affecting official outcomes, and measured one-versus-two-worker runs document queue throughput and game tick cost with safe limits retained.

Implementation steps:
- Declare bounded concurrency and resource requests/limits.
- Measure worker restart and duplicate handling in deployment.
- Keep one worker if two exceed the reference tick budget.

## T5: Validate fun, reliability and an offline release

Milestone: OTL M5 - Release frozen. Pass pair playtests, measured performance/failure gates and offline rehearsals before freezing.

### S14: Playtest and tune the competitive tradeoff

HITL | core | Due 2026-11-12 | Blocked by: S3

Run short pair sessions, record confusion and rematch desire, and tune load, steering and deadline rather than adding features.

Acceptance: Given three pairs playing two rounds each with control sides swapped, notes record result comprehension and rematch choice; at least two pairs understand why they won/lost and choose another run, or a concrete retest/tuning action remains open.

Implementation steps:
- Observe without a narrated tutorial.
- Record spills, finishes, confusion and actual rematch choice.
- Version tuning changes and repeat failed usability checks.

### S15: Measure online quality and abuse boundaries

AFK | core | Due 2026-11-27 | Blocked by: S5, S6, S10, S11, S13, R1

Run the named-hardware two-player reference load with analysis active and network faults; test malformed input, seat isolation, deadline authority and resource bounds.

Acceptance: Given the release candidate running two independent two-player rooms with analysis active for 15 minutes on recorded hardware, p95 aggregate authority step work stays below 16.7 ms without a growing backlog and clients reach 30 FPS, while collision/network/abuse fixtures preserve correct separate results; the public cap never exceeds measured capacity.

Implementation steps:
- Record build, hardware, browser, room count and worker workload.
- Measure aggregate tick work, event-loop delay, correction spikes, frame rate and queue/disk bounds.
- Reject excess admissions and cross-room messages; publish the supported cap and any remaining limitations.

### S16: Package a fully offline two-player fallback

AFK | core | Due 2026-11-27 | Blocked by: S8, S9, S11

Bundle runtime dependencies, licensed assets, images and verified fixtures; use the same service images with Compose and local split-screen.

Acceptance: Given a clean demo browser with external networking disabled and the prepared offline package, two humans complete a local race and inspect a verified replay/Cargo Lab fixture without CDN, remote font or model requests.

Implementation steps:
- Preload images and all browser assets.
- Document start/reset/recovery on primary and spare machines.
- Verify cold-start operation with external networking blocked.

### S17: Rehearse, document and freeze the release

HITL | core | Due 2026-11-27 | Blocked by: S14, S15, S16

Perform three complete rehearsals, record known limitations, prepare the demo narrative and freeze a tagged build with a fallback recording.

Acceptance: Given the release candidate, three full rehearsals including one broker interruption and one offline fallback finish successfully; the tagged build, checksums, runbook and demo recording are available and no blocking issue remains untracked.

Implementation steps:
- Rehearse gameplay, replay, brake comparison and recovery.
- Prepare concise architecture and measured evidence.
- Tag the reviewed release and record submission status separately.

## T6: Deliver the live demo and optional expansion

Milestone: OTL M6 - Live presentation. Present the frozen two-player release. Add optional four-player support only after core evidence passes.

### S18: Present the frozen entry and record the outcome

HITL | core | Due 2026-11-29 | Blocked by: S17

Use the frozen build and rehearsed fallback for the November 29 presentation and Q&A; do not introduce last-minute features.

Acceptance: Given the prepared release/runbook, the live presentation demonstrates the competitive loop and truthful engineering evidence, and the actual demo/Q&A outcome is recorded.

Implementation steps:
- Check devices, keyboard and offline fallback.
- Run the rehearsed presentation.
- Record outcome and follow-up issues without rewriting history.

### X1: Stretch: expand a proven room to four humans

AFK | stretch | Due 2026-11-27 | Blocked by: S15, S17

Only if core release gates are already met, extend room limits/HUD to four humans using identical rules and shared-track rival collisions. Re-run release evidence for any inclusion.

Acceptance: Given four independent browsers, all players ready, race and rematch with matching results and the same measured performance targets; otherwise the shipped limit remains two and this optional issue stays open.

Implementation steps:
- Extend seat capacity without changing score rules.
- Check readability and all-pairs token isolation.
- Re-run performance and freeze a new reviewed tag only if accepted.
