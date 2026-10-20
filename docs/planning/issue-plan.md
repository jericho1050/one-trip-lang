# Issue plan

Initial baseline. GitHub numbers and live hierarchy are in tracking.md. Each child has one observable acceptance scenario; implementation checklists are supporting steps, not separate acceptance tests.

## T1 Planning baseline, rules and asset direction

Milestone: M0 Planning and rules. Outcome: Planning documentation and rules/assets evidence are ready for development.

### P1 Record event rules, submission status and development gate

Mode: HITL. Milestone: M0 Planning and rules. Stories: 24. Dependencies: None.

Record proposal submission/selection status from evidence, known event dates, asset/AI constraints and any unanswered organizer questions. Default application development to November 4 unless earlier permission is documented. Do not send messages or submit forms without authorization.

Acceptance: Given the announcement and available organizer responses, when the rules record is reviewed, then it distinguishes confirmed rules from unknowns and gives an unambiguous permitted development date without claiming unverified submission or selection.

Fallback: Keep the conservative November 4 gate when earlier permission is unavailable.

### P2 Select licensed asset candidates and map the complete user flow

Mode: HITL. Milestone: M0 Planning and rules. Stories: 3, 8, 13, 17, 23. Dependencies: None.

Produce a linked shortlist for room props, slipper, cockroach and audio with license evidence, plus low-fidelity lobby-to-Court and failure-state screens. Do not implement the game before its start gate.

Acceptance: Given the asset shortlist and state map, when the owner reviews them, then both hero assets have verified usable licenses and every PRD player state has a readable screen description.

Fallback: Reduce room props and polish; report missing licensed hero assets as an unresolved blocker.

## T2 A reproducible authoritative throw

Milestone: M1 Reproducible shared throw. Outcome: One visible throw has an authoritative score and reproducible durable evidence.

### S1 Launch one playable graybox throw through the shared simulation

Mode: AFK. Milestone: M1 Reproducible shared throw. Stories: 3, 4, 6. Dependencies: P1.

At the permitted start date, initialize the pinned toolchain and headless simulation, then drive one browser scene from it. Aim, set power/spin, release, collide and auto-return. Keep render frames separate from fixed ticks.

Acceptance: Given a fresh checkout and supported browser, when the documented start command runs and a player throws, then the slipper follows the shared fixed-tick simulation, produces a visible hit or miss and returns under the legal-action rules.

Fallback: Use temporary shapes and gravity/drag only; preserve the independent simulation driver.

### S2 Record and reproduce a throw across the supported runtime matrix

Mode: AFK. Milestone: M1 Reproducible shared throw. Stories: 16, 21. Dependencies: S1.

Add versioned snapshots, canonical hashes, seeded inputs and a replay fixture runner exposed through CI and a minimal replay view. Compare Node, Chromium, Firefox and WebKit using the same pinned build.

Acceptance: Given a saved 10,000-tick fixture, when it runs and is restored midstream on every supported runtime, then finalized checkpoint hashes match and a deliberate state mutation is detected.

Fallback: Simplify custom forces; do not weaken determinism or silently drop a browser.

### S3 Finalize an authoritative scored throw with durable evidence

Mode: AFK. Milestone: M1 Reproducible shared throw. Stories: 5, 6, 16. Dependencies: S2.

Connect one browser to authority, validate inputs, display provisional then finalized hits, and persist an event/replay batch through the asynchronous worker boundary. Add minimal outbox scaffolding without waiting inside ticks.

Acceptance: Given one connected player, when a legal throw hits and leaves the rollback window, then one finalized shared team point and a matching replay event survive a results-service restart without duplicate award.

Fallback: A plain HUD and one local SQLite-backed result process are sufficient.

## T3 Shared multiplayer with bounded reconciliation

Milestone: M2 Complete mixed bout. Outcome: Multiple clients agree on outcomes, recover within documented limits and preserve role privacy.

### S4 Play the same authoritative room in two browsers

Mode: AFK. Milestone: M1 Reproducible shared throw. Stories: 1, 2, 5. Dependencies: S3.

Implement room codes, seats, readiness and snapshots so two clients observe the same legal inputs, target and finalized outcome. Complete the direct WebSocket path.

Acceptance: Given two browsers in one room, when either launches a legal throw, then both show the same finalized throw attribution, shared team score and tick.

Fallback: Single active room on one server; no matchmaking.

### S5 Reconcile within-window late input and reject stale input visibly

Mode: AFK. Milestone: M1 Reproducible shared throw. Stories: 4, 5, 21. Dependencies: S4.

Implement eight-tick rollback, local prediction, corrected snapshots and deterministic latency injection with timing metadata. Keep irreversible facts behind the finalization horizon.

Acceptance: Given a scripted latency fixture, when one input arrives inside the rollback window and another after it, then the first converges to the expected authoritative result and the second is explicitly rejected without changing finalized scores.

Fallback: Limit predicted effects; never pretend a 250 ms delay fits the initial rollback window.

### S6 Reconnect a human seat without leaking hidden roles

Mode: AFK. Milestone: M2 Complete mixed bout. Stories: 9, 15. Dependencies: S4.

Add participant/operator message separation, reconnect tokens, grace timer and disconnected-seat UI. Preserve human seat identity; expired humans idle or leave at bout boundary.

Acceptance: Given a player disconnected within the 15-second grace period, when they resume with the valid token, then they regain the same seat and current state while captured participant messages expose no bot identity or operator secrets.

Fallback: No mid-bout human replacement; use explicit idle state after expiry.

## T4 Air-sensing cockroach in a readable sala

Milestone: M2 Complete mixed bout. Outcome: Orientation affects detection and the player can see why.

### S7 Make slipper orientation drive the cockroach escape model

Mode: AFK. Milestone: M2 Complete mixed bout. Stories: 7. Dependencies: S2, S3.

Implement simplified orientation-dependent air disturbance, sourced sensing parameters, reaction timing and deterministic escape choices. Record cockroach actions alongside player inputs. Use fixture measurements, not handoff spike claims.

Acceptance: Given matched face-on and edge-on approach fixtures, when the simulation runs, then the measured detection timing differs in the expected direction and every escape decision reproduces on replay.

Fallback: Use constrained spin and drag; no lift, tumbling or CFD required.

### S8 Show the sensing evidence in a recognizable sala

Mode: HITL. Milestone: M2 Complete mixed bout. Stories: 3, 7, 8, 23. Dependencies: S7, P2.

Import selected assets, maintain simple colliders, compose the room and add replay wind/threshold/escape overlays. Bundle assets locally and record provenance.

Acceptance: Given the licensed room and hero assets, when a reviewer watches the paired throw fixture at the gameplay camera, then they can identify the slipper and cockroach and explain the detection difference from the visible overlay.

Fallback: Fewer props and simple transform animation; retain silhouette and sensing evidence.

## T5 Hidden bot clients and a complete spotting round

Milestone: M2 Complete mixed bout. Outcome: Bots occupy queued seats and a full mixed bout reaches a truthful reveal.

### S9 Run a budgeted planner as an ordinary game client

Mode: AFK. Milestone: M2 Complete mixed bout. Stories: 10, 11. Dependencies: S4, S7.

Implement candidate-flight planning from public snapshots only, report actual candidate counts, cap work by count and deadline, and send legal inputs through the public connection.

Acceptance: Given low/high budgets and a forced timeout fixture, when the bot plans throws, then telemetry stays within each budget and deadline, inputs obey human limits, and timeout produces a legal fallback without privileged state access.

Fallback: Use a small sampled candidate set; no global search or LLM.

### S10 Assign bot seats through RabbitMQ with fenced fallback

Mode: AFK. Milestone: M2 Complete mixed bout. Stories: 2, 20. Dependencies: S9, S6.

Implement seat jobs, claim/ack lifecycle, heartbeat lease, epoch fencing and understudy client. Test unclaimed work, duplicate delivery and worker failure through the playable room.

Acceptance: Given a pending bot seat and a deliberately lost worker, when the claim deadline or lease expires and a late duplicate worker reconnects, then exactly one current bot client controls the seat and the room remains playable.

Fallback: Host the understudy in a separate worker context; omit fleet orchestration.

### S11 Add bounded reaction and aim variation to bot clients

Mode: AFK. Milestone: M2 Complete mixed bout. Stories: 12. Dependencies: S9.

Add seeded reaction delay, smoothly changing aim and bounded error under the same legal action limits. Expose an operator-only comparison toggle and log observable traces.

Acceptance: Given a fixed bot fixture, when humanization is toggled on, then the trace gains the configured reaction delay and bounded aim progression while remaining replayable and within the planning/action limits.

Fallback: Use simple delays and smoothing; no Fitts-law fitting or behavioral learning.

### S12 Finish a mixed bout with private ballots and reveal

Mode: AFK. Milestone: M2 Complete mixed bout. Stories: 9, 13, 14. Dependencies: S6, S10, S11.

Deliver timed bouts, hidden one-or-two-bot composition, bot/human/abstain ballots, freeze and reveal, and a shared team squash total and separate personal spotting results. Ensure votes and role data stay private until closure.

Acceptance: Given a complete four-seat bout with a repeated ballot and a late edit, when the ballot closes, then the repeat has one effect, the late edit is rejected, identities reveal only after freeze, and displayed shared team and personal spotting totals match the scoring rules.

Fallback: One bout per match, no individual hit ranking and shared spotting awards on ties; no confidence scoring.

## T6 Recoverable results and verified playback

Milestone: M3 Evidence and recovery. Outcome: Broker failure delays effects without changing play; playback is verifiably versioned.

### S13 Recover durable results after a broker outage

Mode: AFK. Milestone: M3 Evidence and recovery. Stories: 19, 21. Dependencies: S3, S10, S12.

Finish outbox publishing, confirmations, transaction-safe duplicate handling, bounded retry/dead letters and pending-result UI. Exercise spool limits and storage-error signaling.

Acceptance: Given a four-seat bout and a 60-second broker outage with duplicate redelivery, when the broker recovers, then ticks continued, every durably acknowledged result appears once in effect, and the spool-limit fixture reports degraded state instead of silently losing facts.

Fallback: Bound the supported outage and refuse the next bout when storage is exhausted; no HA claim.

### S14 Serve a versioned verified replay and reject tampering

Mode: AFK. Milestone: M3 Evidence and recovery. Stories: 16, 21. Dependencies: S2, S12, S13.

Complete replay export, version check, playback and verification badge. Guard public replay access until reveal and show unsupported/corrupt states clearly.

Acceptance: Given a completed bout, an altered copy and an unsupported-version copy, when each is loaded, then the original reproduces its checkpoint hashes while the other two show explicit failure or incompatibility rather than a verified badge.

Fallback: One current simulation version and local replay files; no archive migration.

## T7 Slipper Court with visible conditional evidence

Milestone: M3 Evidence and recovery. Outcome: A controlled lag complaint produces a reproducible comparison and understandable verdict.

### S15 Compute factual and delay-removed Court evidence

Mode: AFK. Milestone: M3 Evidence and recovery. Stories: 17. Dependencies: S5, S7, S14.

Implement the documented controlled intervention, baseline verification, fixed other-player inputs, re-evaluated cockroach decisions and stable random streams. Produce structured evidence, not prose-only verdicts.

Acceptance: Given supported and rejected excuse fixtures plus a fixture missing delay metadata, when Court analyzes them, then the factual branch matches the replay, the alternate changes only the declared intervention and downstream consequences, and verdicts are supported, rejected and inconclusive respectively without changing official scores.

Fallback: Restrict to one claimant and three-second horizon; no arbitrary network diagnosis.

### S16 Present Court comparison and verdict in the player flow

Mode: HITL. Milestone: M3 Evidence and recovery. Stories: 18. Dependencies: S15, S8.

Add a complaint action, paired or toggled trajectories, injected-delay labels, fixed-other-player assumption, clear verdict and offline template dialogue. Display inconclusive states.

Acceptance: Given all three Court fixtures, when a reviewer opens each case from the replay flow offline, then they can identify the factual/alternate result, deliberate delay, key assumption and verdict without reading debug logs.

Fallback: Use preset dialogue and a toggle rather than synchronized split screen; LLM is excluded from core.

## T8 Offline release, rehearsals and live delivery

Milestone: M5 Live presentation. Outcome: The frozen release is measured, rehearsed, submitted when authorized and presented.

### S17 Package the complete game for an offline demo

Mode: AFK. Milestone: M4 Submission ready. Stories: 22, 23. Dependencies: S13, S14, S16.

Provide Compose startup, local assets, preloaded images, seed fixtures, operator credentials setup and a runbook for primary/spare machines. Include a cold-start smoke check.

Acceptance: Given a prepared demo machine with internet disconnected, when the runbook is followed, then a fresh room completes play, spotting, Court and replay verification without any external request being required.

Fallback: Use one machine with local browser sessions if private LAN fails; keep the offline path complete.

### S18 Validate performance, usability and hidden-role isolation

Mode: HITL. Milestone: M4 Submission ready. Stories: 3, 4, 9, 21, 22. Dependencies: S12, S16, S17.

Run four-seat load, worker/broker interruptions, participant payload inspection and manual throw/spotting playtests. Record hardware, versions, p95 tick cost, frame rate and issues.

Acceptance: Given the release candidate on documented demo hardware, when the acceptance suite and manual flow run, then p95 tick time is below 16.7 ms, gameplay remains readable at at least 30 FPS, role isolation passes and any core usability failures have linked fixes.

Fallback: Reduce cosmetic assets, effects and bot budgets; do not hide failed performance targets.

### S19 Rehearse three complete runs and freeze the submission release

Mode: HITL. Milestone: M4 Submission ready. Stories: 22, 24. Dependencies: S18.

Run three end-to-end offline rehearsals, record evidence, prepare fallback video/replay, tag the release and assemble organizer-required submission material. Do not submit externally without authorization.

Acceptance: Given the same release candidate, when three consecutive scripted offline rehearsals finish, then each completes without a core failure and the tagged submission package contains verified assets, replay fixtures, setup steps and fallback media.

Fallback: Drop optional presentation flourishes; core failures reset the clean-run count.

### S20 Present the frozen release and record demo outcome

Mode: HITL. Milestone: M5 Live presentation. Stories: 22, 24. Dependencies: S19.

Use the release/runbook for November 29, explain the model and Court assumptions honestly, and record results and follow-up questions. Requires the entrant; no agent can mark a live presentation complete in advance.

Acceptance: Given the frozen release and fallback kit, when the entrant completes the live presentation, then the outcome record includes what was demonstrated, any fallback used and the Q&A follow-ups.

Fallback: Use labeled verified replay or video if live hardware fails; do not present a recording as live.
