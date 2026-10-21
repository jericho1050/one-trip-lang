# One Trip Lang - Milestones and UI Fidelity

All dates are 2026, Asia/Manila. These are target integration gates for a solo, agent-assisted effort, not person-day estimates. November 4-27 is the 24-day development window supplied by the user. Planning and an explicitly requested local design prototype exist before that window; competition eligibility is not inferred.

| Milestone | Due | Observable exit gate | UI fidelity |
| --- | --- | --- | --- |
| OTL M0 - Proposal and product baseline | Oct 21 | Updated proposal prepared; owner records submission and prework eligibility status. PRD, epic and dependency graph exist. Submission is a human action. | Local split-screen graybox available; no polish claim. |
| OTL M1 - Playable local race | Nov 7 | Two local players complete/rematch with physical cargo, one-time penalties and correct ranking. Shared simulation replay fixture passes. | F1: clear controls, camera, gates, timer and loss feedback in graybox. |
| OTL M2 - Two-player online race | Nov 12 | Two browsers join/ready/race/reconnect/rematch with matching results. Early pair playtests identify and fix confusing controls. | F2: complete room-to-rematch flow; useful error, DNF and disconnected states. |
| OTL M3 - Evidence and useful analysis | Nov 18 | A verified race replay, one honest brake comparison and broker-outage/duplicate-job recovery are demonstrated. | F3: replay and comparison explain what changed; pending/failure states work. |
| OTL M4 - Hosted and recognizable | Nov 23 | Repeatable K3s deployment and worker recovery run without stalling the race; licensed groceries, road, sound and HUD are readable. | F4: consistent low-poly art, legible opponents and cues, mute and credits. |
| OTL M5 - Release frozen | Nov 27 | Named-hardware performance and adverse-network checks pass; three complete rehearsals and offline kit verified; release tagged. | F5: no blocking confusion, clipping or unreadable result states; frozen presentation build. |
| OTL M6 - Live presentation | Nov 29 | Frozen build demonstrated with gameplay, replay evidence and one failure-recovery example; Q&A outcome recorded. | No feature changes during presentation. |

## Priority and cuts

Protect the race before presentation extras. Two humans, understandable losses, the deadline and rematch are the fun test. No authority, broker or analysis work can excuse a broken driving experience.

Cut in order: four-player stretch; extra art/audio variety; extra Cargo Lab profiles and metrics; extra track detail. Keep one verified analysis scenario, one course and one tested deployment. Do not quietly substitute offline racing for the online acceptance gate. If a protected commitment fails its deadline, record a scope decision and update the proposal rather than marking it done.

## Human fun gate

Ask three pairs to play two rounds without a narrated tutorial. Record time to first purposeful turn, misunderstood penalties, finishes versus DNF, and whether both players choose to rematch. Suggested gate: at least two pairs understand the result and voluntarily want another run after the second. This is a small usability signal, not evidence of retention or market fit.

Use deadline/steering/load tuning to repair the core before adding complexity. Swap control sides once to separate keyboard familiarity from game difficulty. Some keyboards cannot register every simultaneous combination; test the actual demo keyboard and keep second-keyboard/online fallback available.

## Demo shape

1. Explain the silly problem in one sentence: “One trip, even if it costs the eggs.”
2. Two players race; show one spill deduction and the result rule.
3. Replay the loss and show the tested earlier-braking comparison with its assumptions.
4. Stop an analysis worker or broker; show the race continuing and background work recovering.
5. Show the versioned infrastructure definition and measured evidence briefly. End on a rematch invitation, not a wall of architecture.
