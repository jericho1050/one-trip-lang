# One Trip Lang - Product Requirements

Status: approved collision-racing direction and delegated implementation baseline, October 21, 2026; ADR 0008. Owner: Jericho / repository owner. This records the approved competitive direction and delegated engineering recommendations. Numerical tuning values and performance budgets are targets, not measured promises.

## Problem Statement

Carrying groceries in more than one trip is apparently unacceptable. Friends would rather race overloaded shopping trolleys home, sacrificing the eggs to save a few seconds.

The real product goal is a short, understandable, replayable competitive browser game. The user preferred driving the One Trip Lang 3D prototype over the fridge-packing alternative. They explicitly chose individual trolleys, starting points reduced by spills, and a shared deadline. Fun with friends comes first. The Wackathon theme is “Useless Problems. Serious Engineering.” Its supplied judging weights are technical creativity 30%, wackiness 25%, surprise 20%, execution 15%, and presentation 10%; this plan cannot guarantee selection or a prize.

## Solution

Two friends race the same short 3D grocery course. Each has an identical preloaded trolley. Accelerate, steer, brake and ram rivals through a bump and two corners, cross ordered gates, and reach home before the shared deadline. Deliver the most grocery points; finish time breaks a points tie.

Ship two-player online rooms plus a two-player local fallback. Four online players are stretch. No shopping, inventory management, walking characters or cargo rearrangement is required for the first release.

### Rules and defaults

| Area | Baseline |
| --- | --- |
| Round | Ready state, 3-second synchronized countdown, race, results, rematch. |
| Course | One compact route, one bump, two ordered corner gates and one finish. Leaving the road slows the trolley; gates prevent shortcut finishes. |
| Load | Six identical groceries in identical positions for every competitor. Host can choose stacked or spread-out preset before readiness; any change clears ready states. |
| Points | Start at 100: eggs 20, milk 15, rice 20, fruit 15, cake 20, cans 10. Values are tuning defaults. |
| Spill | First contact between an item and forbidden ground, or leaving the simulation bounds, permanently loses that item's points exactly once. Wobbling or jumping does not count as a spill. Lost items cannot be collected for points. |
| Finish | Server validates ordered gates and crossing of the finish trigger before the deadline. At that tick, an unlost item's center must be inside the documented delivery volume above its owner's deck; otherwise its points are lost. This stops an airborne grocery behind the trolley from counting as delivered. |
| Deadline | Initial local playtest default 45 seconds after GO, excluding countdown. Production duration is tuned through human playtests. At the exact deadline, a still-racing player is DNF. |
| Ranking | Any valid finisher outranks any DNF. Finishers sort by grocery points descending, then authoritative finish tick ascending. Exact equality is a shared placing. All-DNF means no winner. DNF rows may display remaining points but do not award a victory. |
| Zero points | May still finish; no separate elimination system. |
| Bounds recovery | If the trolley leaves the legal simulation bounds, return it to its last passed gate, lose remaining cargo points and keep the clock running. No score restoration. |
| Contact | Trolleys and groceries physically collide with rivals in the same room. Both loads are at risk; a bump alone has no score penalty. Ownership never transfers, even if cargo lands on a rival. Finished/DNF racers and all their cargo leave the active collision world immediately after outcome resolution. Separate start slots prevent initial overlap. |
| Feel | Stacked cargo visibly rocks on side-swipes and can spill in hard crashes. A full idle round retains all cargo; a reproducible careful run retains at least 80 points. Physical pitch/roll with damped recovery is required. No glued stacks or random spill penalties. |
| Rooms | Two human seats per private room; separate physics world, clock, scores and replay per match. One server process may host several rooms up to its tested cap. Online clients each render their own follow camera. |
| Controls | Local P1 WASD, P2 arrows. W/up accelerates, A/D or left/right steers, S/down brakes; holding brake at rest reverses. Online each player chooses either mapping. |
| Pause | Local split-screen pauses both players together and auto-pauses on focus loss. Online has no player-controlled pause: the server's race clock continues. |
| Disconnect | Neutralize stale controls; allow the same seat to reconnect for an initial 10-second grace while the race clock and physics continue. After grace the player is DNF and removed from active collisions. No bot takeover. |
| Rematch | Same room; clear inputs, lost flags, times and scores; all players ready again. No mid-race joins. |

The intended tradeoff is speed versus cargo preservation. Braking is legitimate strategy. The deadline should prevent an entire race at a crawl, while allowing careful corners. If everyone can effortlessly retain 100 points, change load/route/timing before adding features.

### Serious engineering visible in the product

1. **Authoritative race:** every client agrees on spills, deadline and winner. Clients send controls, never their own scores.
2. **Verified replay:** replay the accepted race inputs against the recorded simulation version and compare state hashes and score events.
3. **Cargo Lab:** after results, optionally compare the factual run with a small set of explicitly modified braking inputs. Show whether a tested variant retained more cargo and still finished in time. This is a bounded search, not a proof of an optimal route or what a human would have done.
4. **Background resilience:** RabbitMQ carries results, replay verification and Cargo Lab work. A stopped broker or killed analysis worker cannot freeze a live race. Pending analysis is visible and retryable.
5. **Reproducible hosting:** IaC and a small Kubernetes deployment recreate the demo and constrain analysis workers so they do not consume the live game's budget.

### Never-cut scope for this product

Playable 3D trolley handling; two concurrent humans; equal starting conditions; physical cargo and meaningful ramming; isolated rooms and individual POVs; understandable one-time score loss; shared deadline and correct rankings; server authority for online play; versioned replay evidence; RabbitMQ outside the tick; offline/local fallback; documented asset rights. Cargo Lab's smallest verified brake comparison and basic IaC/K3s deployment are planned engineering commitments, with gameplay completed first.

## User Stories

1. As a player, I want to understand the goal before starting so I can race without reading a manual.
2. As two people at one computer, we want independent WASD and arrow controls so we can play simultaneously.
3. As a host, I want a room code so a friend can join without an account.
4. As a player, I want readiness and a common countdown so nobody gets an early start.
5. As a player, I want the same load and course as my rival so the comparison is fair.
6. As a player, I want acceleration, steering, braking and reversing so I can recover from a bad corner.
7. As a player, I want groceries to visibly shift and fall so I understand the risk of speed.
8. As a player, I want a named point deduction only when cargo is lost so scoring feels explainable.
9. As a player, I want a visible shared clock so I can judge how cautiously I can drive.
10. As a player, I want clear corner gates and a finish marker so I know where to go.
11. As a player, I want a readable camera and unobstructed local trolley so I can judge turns.
12. As a player, I want the same score and winner on both screens so the competition is trustworthy.
13. As a player, I want DNF and tie rules explained so I understand the result.
14. As a player, I want one-button rematch and readiness reset so we can try again quickly.
15. As a disconnected player, I want a limited chance to reclaim my seat without stopping my rival's clock.
16. As a player, I want a verified replay of my spill so I can inspect what happened.
17. As a curious player, I want to test an earlier-braking variant after the race so the extra simulation is useful.
18. As a player, I want analysis to fail or queue without disrupting racing.
19. As an operator, I want duplicate jobs and worker crashes handled without duplicate scores or conflicting analyses.
20. As an operator, I want bounded queues, input validation and resource limits so the demo stays responsive.
21. As a presenter, I want an offline two-player fallback and rehearsed fixtures so the demo can survive venue internet problems.
22. As a maintainer, I want reproducible deployment and documented teardown so hosting is repeatable and costs are controlled.
23. As a player, I want recognizable groceries, clear sound feedback and mute so the experience reads quickly.
24. As a maintainer, I want licensed assets and tracked acceptance evidence so the entry is explainable and releasable.
25. As a future group of four friends, we want a larger room using the same rules once the two-player game is stable. This story is stretch.
26. As a player, I want to ram a rival and risk my own cargo so overtaking involves a tactical choice.
27. As a player, I want impacts to visibly rock the load while careful driving remains viable so the physics feels understandable.
28. As a group, we want our private room to have its own race so another match cannot affect ours.
29. As a player, I want finished and expired racers to clear the road so they cannot block my finish indefinitely.
30. As an operator, I want a tested room limit and a clear server-busy response so excess joins cannot overload active races.

## Implementation Decisions

- A TypeScript monorepo with Vite, Three.js and a lightweight HTML HUD. Reuse direct Three.js from the prototype; React is unnecessary for this small UI. No custom renderer, physics engine or networking framework.
- The exploratory preview uses Three.js and cannon-es with a dynamic, vertically guided trolley and damped pitch/roll. Production recommendation: pinned Rapier WASM and a headless shared simulation. Use a dynamic collision-responsive chassis, arcade drive forces, simple vertical support and a damped pitch/roll spring. Preserve the approved feel; a wheel-by-wheel vehicle simulator is out of scope.
- Deep modules: race simulation (controls, cargo, gates, state machine); authority/session protocol; replay/verifier; result persistence and outbox; bounded Cargo Lab planner; renderer/HUD; deployment/asset manifest. Rendering has no authority over results.
- Node.js with Colyseus for room lifecycle, seats, reconnection and direct WebSocket transport. Custom authoritative physics snapshots remain explicit; the framework does not prove physics correctness. Fixed 60 Hz simulation and initial 20 Hz snapshots. Predict the small interacting world from complete authoritative snapshots and reapply pending local controls with bounded remote-input extrapolation. Reconcile all colliding bodies together; confirm scores only from the server. No server rollback or GGPO replication is required in v1. Late controls affect future admitted ticks, never rewrite finalized points.
- Server-owned integer ticks for countdown, deadline and finish ordering. Stable IDs, input sequencing, versioned load/course configuration and pinned engine. No wall clock, I/O or platform-dependent trigonometry in the authoritative core; use a committed direction lookup for quantized heading.
- Separate game authority, results/replay service and analysis worker processes. RabbitMQ handles background events/jobs only. Per-service SQLite and bounded durable spool; persistent volumes and idempotency keys. No distributed database platform.
- Cargo Lab restores the whole match, edits one player’s brake controls and resimulates all colliding bodies with rivals’ recorded controls fixed. Test at most 16 profiles under bounded simulation and wall-clock budgets. Label this assumption; a rival might react differently in real play. Live scores never change.
- One VPS, K3s, OpenTofu for provider resources and cloud-init for host bootstrapping; Docker Compose for local/offline fallback. Basic manifests, readiness probes and limits. No service mesh, managed Kubernetes cluster or autoscaling platform.
- Free licensed grocery/environment assets with simple collider proxies. No manual character modeling. AI-generated cosmetics are optional; no runtime AI API dependency.
- Existing GitHub repository is retained under its historical slug; the One Trip Lang label, docs, epic and milestone prefix distinguish the new plan. Historical Tsinelas requirements do not become implementation dependencies.

### Acceptance targets, not measured results

- Two humans can join, ready, complete and rematch one online race with consistent final scores.
- Scripted spill, collision, cargo ownership, finished/DNF clearing, room isolation, deadline, finish-volume, ranking, duplicate-input and disconnect scenarios pass.
- A versioned side-swipe produces visible physical cargo tilt (initial target at least 8 degrees), a hard impact spills cargo, 45 seconds of idle retains 100 points, and a careful course run retains at least 80. These are production test targets based on prototype regressions, not transferred Rapier measurements.
- Two concurrent two-player rooms run independently; crossing room/seat tokens is rejected and disposing one room does not reset the other. Public admission initially caps at one room until multi-room load evidence supports a higher configured cap.
- A version-pinned 10,000-tick replay fixture matches authoritative hashes in Node and supported desktop Chromium. Firefox/WebKit support follows verified compatibility, not assumptions.
- Reference staging load of two independent two-player rooms sustains 60 Hz for 15 minutes with p95 aggregate authority step work below 16.7 ms and no growing backlog; target at least 30 FPS on named demo hardware. Profile with Cargo Lab active, record overruns/correction spikes, and keep public admission at or below measured capacity. Capture build, hardware and workload with every claim.
- At simulated 150 ms RTT and 30 ms jitter, clients converge to the same authoritative result. This is an initial test target, not a promise of invisible latency.
- A 60-second RabbitMQ outage does not stall the live race; recovery publishes a single effective result per match. Disk exhaustion reports degraded state and prevents new matches rather than pretending persistence succeeded.
- Cargo Lab reproduces its factual baseline before showing an alternative; corrupted/unsupported replay is rejected. Duplicate deliveries and worker restart produce one effective result per analysis key.
- Three complete rehearsals, including offline fallback and one broker interruption, pass before release freeze.

## Testing Decisions

Test externally visible outcomes and failure boundaries. Automate simulation/rules fixtures, input admission, replay restoration, finish ordering, outbox deduplication, worker redelivery and browser room flows. Use Vitest, Playwright and real RabbitMQ/SQLite integration fixtures. Tests should fail on wrong player-visible behavior, not implementation rearrangement.

Human review covers steering feel, camera readability, whether spills are understood, and whether people want a rematch. Target three independent pairs, two runs per pair; this is an exploratory usability gate, not statistical proof of fun. Record confusion and changes. If it fails, simplify/tune before adding four-player support.

Existing evidence is limited to local prototype checks. There is no production server, network benchmark, deterministic Rapier migration, deployment or real two-human usability validation yet. The local browser's synthetic simultaneous-key tests do not guarantee every physical keyboard supports all held-key combinations.

## Out of Scope

Core release excludes weapons, combat powers, walking avatars, manual packing, grocery recovery, procedural tracks, public matchmaking, accounts, payments, global rankings, hidden bots, bot guessing, Slipper Court, cockroach biology, chat/voice, mobile gameplay, realistic suspension, server rollback and production high availability.

Four-player rooms and ordinary-client AI practice racers are stretch. No core dependency requires them. Remote LLMs cannot decide physics, score, winner or replay validity. Do not claim an analysis is globally optimal.

## Further Notes

Event dates supplied by the user: proposal October 21; evaluation October 22-26; selection October 27; development November 4-27; live presentation November 29, 2026, Asia/Manila. Submission/selection remain unconfirmed. A refreshed One Trip Lang proposal and organizer clarification about pre-development prototypes are tracked human tasks. The user explicitly authorized this local design prototype; that does not establish competition eligibility or authorize submitting anything on their behalf.

Solo with agent assistance. Milestones are outcome targets, not a capacity guarantee. No weekly-hours assumption. The new competitive product supersedes the earlier cooperative grocery and Tsinelas gameplay. Infrastructure suggestions are adopted as a minimal recommended baseline under the user's delegated decisions; the offered VPS is preferred if it passes the load gate, with a paid Lightsail fallback and estimates in the infrastructure plan. Nothing has been provisioned or purchased.
