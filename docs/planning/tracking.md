# GitHub tracking

Repository: https://github.com/jericho1050/tsinelas-arena

- [PRD](https://github.com/jericho1050/tsinelas-arena/issues/1)
- [Delivery epic](https://github.com/jericho1050/tsinelas-arena/issues/2)
- [Milestones](https://github.com/jericho1050/tsinelas-arena/milestones)

All issues start open with needs-triage. Native sub-issue hierarchy and blocked-by links are configured. Do not interpret a task as complete without its acceptance evidence.

## Milestones

- [M0 Planning and rules](https://github.com/jericho1050/tsinelas-arena/milestone/1) - 2026-10-27: Planning baseline, rules gate, asset shortlist and status recorded.
- [M1 Reproducible shared throw](https://github.com/jericho1050/tsinelas-arena/milestone/2) - 2026-11-10: Reproducible authoritative throw and two clients agreeing on outcomes.
- [M2 Complete mixed bout](https://github.com/jericho1050/tsinelas-arena/milestone/3) - 2026-11-17: Humans and bots complete the air-sensing game, ballot and reveal.
- [M3 Evidence and recovery](https://github.com/jericho1050/tsinelas-arena/milestone/4) - 2026-11-24: Verified replay, truthful Court and broker-outage recovery.
- [M4 Submission ready](https://github.com/jericho1050/tsinelas-arena/milestone/5) - 2026-11-27: Offline kit, performance evidence and three rehearsals; release frozen.
- [M5 Live presentation](https://github.com/jericho1050/tsinelas-arena/milestone/6) - 2026-11-29: Live demo and Q&A using the frozen release and fallback kit.

## Tasks and subtasks

### [Planning baseline, rules and asset direction](https://github.com/jericho1050/tsinelas-arena/issues/3)

- [P1 Record event rules, submission status and development gate](https://github.com/jericho1050/tsinelas-arena/issues/11) - HITL; blocked by none.
- [P2 Select licensed asset candidates and map the complete user flow](https://github.com/jericho1050/tsinelas-arena/issues/12) - HITL; blocked by none.

### [A reproducible authoritative throw](https://github.com/jericho1050/tsinelas-arena/issues/4)

- [S1 Launch one playable graybox throw through the shared simulation](https://github.com/jericho1050/tsinelas-arena/issues/13) - AFK; blocked by #11.
- [S2 Record and reproduce a throw across the supported runtime matrix](https://github.com/jericho1050/tsinelas-arena/issues/14) - AFK; blocked by #13.
- [S3 Finalize an authoritative scored throw with durable evidence](https://github.com/jericho1050/tsinelas-arena/issues/15) - AFK; blocked by #14.

### [Shared multiplayer with bounded reconciliation](https://github.com/jericho1050/tsinelas-arena/issues/5)

- [S4 Play the same authoritative room in two browsers](https://github.com/jericho1050/tsinelas-arena/issues/16) - AFK; blocked by #15.
- [S5 Reconcile within-window late input and reject stale input visibly](https://github.com/jericho1050/tsinelas-arena/issues/17) - AFK; blocked by #16.
- [S6 Reconnect a human seat without leaking hidden roles](https://github.com/jericho1050/tsinelas-arena/issues/18) - AFK; blocked by #16.

### [Air-sensing cockroach in a readable sala](https://github.com/jericho1050/tsinelas-arena/issues/6)

- [S7 Make slipper orientation drive the cockroach escape model](https://github.com/jericho1050/tsinelas-arena/issues/19) - AFK; blocked by #14, #15.
- [S8 Show the sensing evidence in a recognizable sala](https://github.com/jericho1050/tsinelas-arena/issues/20) - HITL; blocked by #19, #12.

### [Hidden bot clients and a complete spotting round](https://github.com/jericho1050/tsinelas-arena/issues/7)

- [S9 Run a budgeted planner as an ordinary game client](https://github.com/jericho1050/tsinelas-arena/issues/21) - AFK; blocked by #16, #19.
- [S10 Assign bot seats through RabbitMQ with fenced fallback](https://github.com/jericho1050/tsinelas-arena/issues/22) - AFK; blocked by #21, #18.
- [S11 Add bounded reaction and aim variation to bot clients](https://github.com/jericho1050/tsinelas-arena/issues/23) - AFK; blocked by #21.
- [S12 Finish a mixed bout with private ballots and reveal](https://github.com/jericho1050/tsinelas-arena/issues/24) - AFK; blocked by #18, #22, #23.

### [Recoverable results and verified playback](https://github.com/jericho1050/tsinelas-arena/issues/8)

- [S13 Recover durable results after a broker outage](https://github.com/jericho1050/tsinelas-arena/issues/25) - AFK; blocked by #15, #22, #24.
- [S14 Serve a versioned verified replay and reject tampering](https://github.com/jericho1050/tsinelas-arena/issues/26) - AFK; blocked by #14, #24, #25.

### [Slipper Court with visible conditional evidence](https://github.com/jericho1050/tsinelas-arena/issues/9)

- [S15 Compute factual and delay-removed Court evidence](https://github.com/jericho1050/tsinelas-arena/issues/27) - AFK; blocked by #17, #19, #26.
- [S16 Present Court comparison and verdict in the player flow](https://github.com/jericho1050/tsinelas-arena/issues/28) - HITL; blocked by #27, #20.

### [Offline release, rehearsals and live delivery](https://github.com/jericho1050/tsinelas-arena/issues/10)

- [S17 Package the complete game for an offline demo](https://github.com/jericho1050/tsinelas-arena/issues/29) - AFK; blocked by #25, #26, #28.
- [S18 Validate performance, usability and hidden-role isolation](https://github.com/jericho1050/tsinelas-arena/issues/30) - HITL; blocked by #24, #28, #29.
- [S19 Rehearse three complete runs and freeze the submission release](https://github.com/jericho1050/tsinelas-arena/issues/31) - HITL; blocked by #30.
- [S20 Present the frozen release and record demo outcome](https://github.com/jericho1050/tsinelas-arena/issues/32) - HITL; blocked by #31.

## Operating the tracker

1. Review planning tasks first; record organizer and asset evidence.
2. At the permitted start date, triage an unblocked subtask and apply ready-for-agent or ready-for-human.
3. Implement one issue per branch/PR, attach acceptance evidence, then close the completed issue.
4. Remove status:blocked only when every prerequisite is satisfied.
5. Close task parents after all core children pass; close milestones only after their exit gate is demonstrated.
6. Propose scope changes through a PR updating the PRD, ADRs and affected issues.
