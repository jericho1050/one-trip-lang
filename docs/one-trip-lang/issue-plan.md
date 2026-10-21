# One Trip Lang - Epic and Implementation Breakdown

This is the readable source plan. Each leaf has one observable acceptance scenario. Mode AFK means specified work; HITL requires human review or action. Neither authorizes early competition implementation. See the published tracking index for real issue links.

## Epic

Deliver a two-human competitive 3D grocery race with fair rules, verified replay, bounded background Cargo Lab, repeatable deployment and an offline demo by the November 27 freeze / November 29 presentation.

Completion: all core child acceptance evidence and the release/demo gates pass. Stretch work cannot block this epic.

## T0: Proposal, rules and asset readiness

Milestone: OTL M0 - Proposal and product baseline. Make the new competitive product and submission status concrete before production implementation.

### P1: Refresh the proposal for the competitive grocery race

HITL | core | Due 2026-10-21 | Blocked by: none

Use the official proposal headings, keep team identity placeholders where unknown, and describe the current game and earned engineering. Record submission separately; do not submit without instruction.

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

HITL | core | Due 2026-10-21 | Blocked by: none

Choose enough assets for one trolley, six groceries, one route/house and minimal cues; validate rights before import.

Acceptance: Given the asset shortlist, every selected file has a source URL, license and required attribution, and a small reference sheet shows the six groceries can be distinguished.

Implementation steps:
- Shortlist reusable low-poly packs.
- Record per-pack rights and attribution.
- Choose simple collider proxies and a minimal visual direction.

## T1: Complete a fair local grocery race

Milestone: OTL M1 - Playable local race. Deliver the complete two-human local loop from ready through points, deadline, result and rematch.

### S1: Drive one trolley through the production course

AFK | core | Due 2026-11-07 | Blocked by: P2

Create the pinned production simulation and browser view with acceleration, braking/reverse, one bump, ordered corner gates and the finish. Reuse libraries; isolate authoritative stepping from rendering.

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

### S3: Play and rematch with independent local controls

AFK | core | Due 2026-11-07 | Blocked by: S2

Add split-screen simultaneous WASD/arrows, identical load presets, common countdown, global local pause and clean rematch.

Acceptance: Given two local players holding different controls concurrently, both trolleys respond independently; after finish/deadline a rematch restores both to 100 points, identical loads, zero elapsed race time and no held input.

Implementation steps:
- Wire two input streams without shared bindings.
- Render independent cameras and readable rival ghosts.
- Reset all state and handle focus-loss pause.

## T2: Race a friend in an authoritative online room

Milestone: OTL M2 - Two-player online race. Deliver a two-browser room with server-owned outcomes and understandable reconnect behavior.

### S4: Join and finish a real two-browser race

AFK | core | Due 2026-11-12 | Blocked by: S2

Implement room code, session ownership, ready/countdown, direct WebSocket controls, authoritative snapshots and consistent result/rematch.

Acceptance: Given two independent browsers joining one room, they ready, race and rematch with identical authoritative spill events, deadline tick and final ranking; a client-sent score cannot change the result.

Implementation steps:
- Create a versioned validated protocol and room lifecycle.
- Advance the shared simulation only on the authority.
- Display lobby, race, results and rematch in both browsers.

### S5: Keep racing responsive under delay and hostile input

AFK | core | Due 2026-11-12 | Blocked by: S4

Predict/reconcile local trolley and cargo; interpolate rivals; validate packet size/rate, ownership, sequence and input expiry. No authoritative rollback.

Acceptance: Given 150 ms RTT with 30 ms jitter plus duplicated, stale and forged-seat inputs, both browsers converge on the same result, rejected input has no unauthorized effect, and a silent client cannot leave throttle stuck indefinitely.

Implementation steps:
- Bound input history and reconnect epoch.
- Reapply unacknowledged local controls after authoritative restore.
- Record latency and correction evidence on the reference build.

### S6: Reconnect a seat without pausing the race

AFK | core | Due 2026-11-12 | Blocked by: S4

Neutralize stale input on disconnect, reclaim the same seat with its token within grace, and mark DNF after grace while rivals keep racing.

Acceptance: Given a dropped connection, resuming within 10 seconds restores the same seat and current clock; a second drop beyond grace produces DNF without stopping the rival or allowing another token to steal the seat.

Implementation steps:
- Implement bounded grace and seat token validation.
- Show reconnecting/expired states.
- Test the race clock and stale-control behavior during loss.

## T3: Verify races and test useful braking alternatives

Milestone: OTL M3 - Evidence and useful analysis. Show truthful replay and bounded Cargo Lab output that survives background-service failures.

### S7: Verify a recorded race against the shared simulation

AFK | core | Due 2026-11-07 | Blocked by: S2

Record versioned initial state, admitted controls, irreversible facts and canonical hashes; restore and verify with a readable replay view.

Acceptance: Given the pinned 10,000-tick fixture, Node and supported Chromium replay matching state hashes and score events; changing an input or using an unsupported version yields a visible verification failure.

Implementation steps:
- Define replay/version envelope and canonical state.
- Implement baseline verification and viewer seeking.
- Capture runtime/build evidence for determinism.

### S8: Publish durable results and replay work outside the tick

AFK | core | Due 2026-11-18 | Blocked by: S4, S7

Create the bounded spool/outbox and RabbitMQ publisher with separate results/replay consumer; unique keys make redelivery harmless.

Acceptance: Given a 60-second broker interruption while a race completes, play continues and shows pending persistence/publication accurately; after recovery exactly one effective result and replay record exists for the match.

Implementation steps:
- Implement asynchronous writer and bounded backpressure states.
- Use persistent messages, publisher confirms and post-commit acknowledgements.
- Exercise broker outage, duplicate delivery and disk-full admission refusal.

### S9: Run a bounded earlier-braking Cargo Lab experiment

AFK | core | Due 2026-11-18 | Blocked by: S7, S8

From a verified replay, queue a maximum 16-profile brake search around one spill and show factual versus best tested candidate with assumptions and limits.

Acceptance: Given one known improvable replay and one non-improvable fixture, the UI shows a verified factual baseline, the exact modified controls, and either a valid tested improvement or no improvement; official race points remain unchanged.

Implementation steps:
- Define immutable analysis key, input profiles and budgets.
- Reuse the same simulation with bounded horizon/timeout.
- Continue a candidate to deadline before claiming an improved finish.

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
- Import optimized assets and license manifest.
- Add restrained cues for start, loss and finish.
- Check camera, overlap ghosts and result readability.

### S12: Deploy one reproducible HTTPS race environment

AFK | core | Due 2026-11-23 | Blocked by: S4, S8, P2

Define OpenTofu/cloud-init and K3s workloads for one VPS, with game/worker boundaries, persistent storage, restricted management and HTTPS/WSS. Actual provider apply requires resolved access/budget.

Acceptance: Given a clean authorized host or disposable equivalent, documented provisioning and deployment bring up a two-browser HTTPS race and background result processing from pinned definitions without undocumented manual changes.

Implementation steps:
- Document provided-host versus provider-managed resources.
- Declare images, volumes, probes, secrets references and ingress.
- Record clean install, teardown and state-handling steps.

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

AFK | core | Due 2026-11-27 | Blocked by: S5, S6, S10, S11, S13

Run the named-hardware two-player reference load with analysis active and network faults; test malformed input, seat isolation, deadline authority and resource bounds.

Acceptance: Given the release candidate on recorded hardware, p95 authority step work stays below 16.7 ms and client frame rate remains at least 30 FPS during the reference two-player/analysis workload, while network/abuse fixtures preserve identical final rankings.

Implementation steps:
- Record build, hardware, browser and workload.
- Measure tick/frame timings separately and exercise network faults.
- Attach security/rate-limit/resource evidence and unresolved limitations.

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

Only if core release gates are already met, extend room limits/HUD to four humans using identical rules and no rival collisions. Re-run release evidence for any inclusion.

Acceptance: Given four independent browsers, all players ready, race and rematch with matching results and the same measured performance targets; otherwise the shipped limit remains two and this optional issue stays open.

Implementation steps:
- Extend seat capacity without changing score rules.
- Check readability and all-pairs token isolation.
- Re-run performance and freeze a new reviewed tag only if accepted.
