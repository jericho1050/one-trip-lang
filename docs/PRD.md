# Tsinelas Arena PRD

Status: initial planning baseline, synthesized from approved recommendations. No functionality is implemented or benchmarked. Owner: repository owner. Event dates: Asia/Manila, 2026.

## Problem Statement

At 2 a.m. there is an ipis in the sala. Everyone throws slippers, misses and blames lag. Some helpful teammates are secretly bots. The intentionally useless problem is squashing the cockroach together, identifying which teammates were machines and testing a controlled lag excuse.

The entry must communicate a ridiculous premise through serious, demonstrable engineering. The supplied judging weights are technical creativity 30%, wackiness 25%, surprise 20%, execution 15% and presentation 10%. Success means a coherent playable demonstration, not a large feature count. Selection and prizes cannot be predicted from this plan.

## Solution

A four-seat cooperative desktop 3D browser game in one Filipino sala. All humans and hidden bots are teammates helping to squash a cockroach whose escape behavior depends on a simplified air field. A spotting ballot follows the bout. Bots do not sabotage play, and the reveal does not eliminate anyone. Slipper Court compares recorded play with a clearly defined controlled-delay experiment.

Priority order: satisfying shared throwing; visible air sensing; hidden bots and spotting; truthful Court; optional LLM dialogue. Use library rendering and collision support, sourced assets and one shared simulation. Keep the user flow to join, throw, vote, reveal and inspect Court.

### Product defaults

- One 90-second bout per match, followed by a 15-second ballot. Values are tunable initial defaults.
- Four seats; random one or two bots, fixed during the bout. Two-human/two-bot composition is a rehearsed operator fixture, not forced in normal play.
- Joining humans fill available human seats; the host can start only when all seats are occupied. Normal play therefore needs two or three humans. A local demo harness can supply two human browser sessions.
- Fixed throwing stations. One active slipper per seat. Direction, power and spin are bounded and quantized; auto-return after rest or a flight timeout; initial cooldown one second after return.
- One shared team point per finalized squash, regardless of who hits. Reset the cockroach at a deterministic legal position after a short visible reset. Record the earliest collision for replay attribution, with stable seat ID resolving exact ties; attribution is not a competitive award.
- Spotting: bot/human/abstain for each teammate. Correct +1, incorrect -1, abstain or missing 0. Show the shared team total and separate personal spotting points. Do not rank teammates by hits; spotting ties may share an award.
- No accounts, payments, global leaderboard or personal profile collection. Room codes and session-scoped reconnect tokens suffice.

## User Stories

1. As a host, I want a room code so friends can join one match.
2. As a player, I want clear seat and ready states so I know when play starts.
3. As a player, I want readable aim, power and spin controls so I understand each throw.
4. As a player, I want immediate visual feedback so throwing feels responsive.
5. As a player, I want one authoritative hit result so every participant agrees on the shared team score.
6. As a player, I want my slipper returned automatically so I can keep playing.
7. As a player, I want the cockroach to respond to the air disturbance so orientation creates a tactic.
8. As a spectator, I want an air-sensing overlay so I understand an escape.
9. As a player, I want bot identities hidden until voting ends so spotting is meaningful.
10. As a player, I want bots bound to my information and action limits so the contest is fair.
11. As an operator, I want measured bot planning budgets so I can demonstrate computational difficulty.
12. As a player, I want bots with bounded reaction and aim variation so their identity is not immediately obvious.
13. As a player, I want to classify teammates or abstain before reveal so guesses can be scored fairly.
14. As a player, I want a shared squash total and separate personal spotting results so cooperation and deduction are both visible.
15. As a disconnected human, I want a brief reconnect opportunity without being silently replaced by a bot.
16. As an operator, I want replay verification tied to a simulation version so claims can be checked.
17. As a player, I want a controlled lag complaint replayed with its assumptions visible so the verdict is honest.
18. As a spectator, I want both Court trajectories and the verdict visible so I can follow the experiment.
19. As an operator, I want broker outages to delay background effects without stopping play.
20. As an operator, I want bot-worker failure handled without duplicate seat ownership.
21. As an operator, I want versioned evidence and bounded telemetry so performance claims are measurable.
22. As a presenter, I want the demo to start and run offline so venue internet is irrelevant.
23. As a maintainer, I want an asset license manifest so every shipped asset has a known source.
24. As a reviewer, I want linked tasks and milestone gates so I can see what is done and what is blocked.

## Implementation Decisions

- TypeScript, Vite and React for the client; Three.js through React Three Fiber and Drei for scene composition. This is a planned wrapper around Three.js, not a replacement simulation engine.
- Rapier WASM with one pinned version and a headless simulation core. Only the explicit fixed-tick simulation driver advances physics. React/render frames never own simulation time.
- Node.js authority with direct WebSocket connections, snapshots, local prediction and bounded rollback. Initial rollback window eight ticks at 60 Hz, subject to profiling. Inputs arriving after finalization are rejected, never silently applied as if on time.
- Simplified slipper drag and orientation-dependent air signal first. Advanced lift, tumbling and full six-degree aerodynamics are stretch work.
- Cockroach decisions generated by a deterministic brain and recorded as actor inputs. Court re-evaluates this brain in its alternate branch; ordinary playback uses the recorded inputs.
- Bots are ordinary clients with observed-state planning, not privileged replicas of hidden server state. Candidate-flight counts and wall-clock deadlines are separate limits.
- RabbitMQ per-seat jobs with lease/fencing protection and an understudy. Separate game authority, bot worker and results/replay consumer processes; telemetry is a bounded consumer, not a new infrastructure platform.
- SQLite owned per service, with idempotent processing and an asynchronous durable outbox boundary. At-least-once delivery; no exactly-once transport claim.
- Versioned replay, role isolation, stable canonical hash inputs and controlled Court branching are core modules. Deep interfaces hide transport, persistence and engine internals from gameplay.
- One private VPS for playtests, Docker Compose locally and on stage. Single broker and host are accepted failure domains, with recovery tests rather than high-availability claims.
- GitHub repository, issue hierarchy and milestones are the planning source of truth. Documentation is versioned alongside future code.

### Measurable completion gates

These are acceptance targets, not achieved measurements.

- A scripted 10,000-tick fixture reproduces hashes across Node, Chromium, Firefox and WebKit on the supported version matrix; any unsupported browser must be explicitly gated before release.
- A four-seat reference load sustains 60 simulation ticks/second with p95 tick processing below 16.7 ms on documented demo hardware; record frame rates separately. Target 60 FPS, minimum readable 30 FPS on that hardware.
- No participant payload exposes roles before ballot freeze. Reject malformed, duplicate and out-of-window actions consistently.
- A 60-second broker outage does not stop an already running bout; acknowledged finalized results are delivered once in effect after recovery.
- Valid replay restores the expected hashes; a modified replay fails verification; unsupported versions are reported rather than silently loaded.
- Both Court outcomes (excuse supported and rejected) have known fixtures and visible assumptions. No scientific validation or general network-diagnosis claim.
- Three complete offline rehearsals pass before optional work is added.

## Testing Decisions

Test public behavior and failure boundaries rather than internal function structure. Automate simulation fixtures, save/restore, cross-engine hashing, input admission, score finalization, identity isolation, ballot idempotency, seat fencing, outbox recovery, replay tamper detection and Court branch comparison.

Use Vitest for logic/integration harnesses and Playwright for supported-browser fixtures and full user flows. Test real RabbitMQ and SQLite recovery in containers. Record performance on named hardware. Manual HITL reviews cover throw feel, visual readability, bot spotting and live presentation. No prior tests or codebase exist yet.

## Out of Scope

Walking/fetching slippers, mobile controls, multiple rooms hosted at scale, public matchmaking, accounts, monetization, persistent global rankings, full fluid simulation, hand-modeled assets, Kubernetes, WebTransport, server crash resurrection, sophisticated biomechanical humanization and voice interaction.

LLM Court dialogue is optional and never determines physical evidence or verdicts. No core task depends on remote model access. Advanced cameras and aerodynamics wait until core acceptance gates pass.

## Further Notes

Proposal deadline October 21; evaluation October 22-26; selection October 27; development November 4-27; final submission November 27; live demo November 29. Submission/selection status and organizer policy on pre-development code remain unverified. Design and documentation may proceed; implementation is gated until November 4 or recorded organizer permission.

The user accepted recommended defaults and controls final scope approval. Do not infer a capacity estimate from solo status or AI assistance. Milestones express desired outcomes, not guaranteed effort. If core feasibility fails, simplify the underlying model and presentation while preserving the never-cut list; record any proposed change to a core commitment before proceeding.
