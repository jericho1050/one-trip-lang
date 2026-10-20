# Milestones and UI fidelity gates

All dates are 2026 in Asia/Manila. Dates are targets, not effort estimates or permission to ignore dependencies. The owner controls capacity; no person-day assumption is used.

| Milestone | Due | Observable exit gate | UI fidelity |
|---|---|---|---|
| M0 Planning and rules | Oct 27 | PRD, technical plan, asset shortlist and rules decision recorded; submission/selection status updated | Low fidelity screen/state map |
| M1 Reproducible shared throw | Nov 10 | One server-scored throw reproduces across supported runtimes; two browsers agree | Playable graybox controls and HUD |
| M2 Complete mixed bout | Nov 17 | Two humans and two bots finish a bout, vote and reveal; air-sensing behavior is visible | Cohesive room and complete core flow |
| M3 Evidence and recovery | Nov 24 | Broker outage recovers results once in effect; verified replay and both Court verdicts pass | Court and failure/reconnect states readable |
| M4 Submission ready | Nov 27 | Offline kit passes performance checks and three rehearsals; final submission package ready | Polish only; no new core feature work |
| M5 Live presentation | Nov 29 | Same release runs through the live script and Q&A with fallback ready | Frozen release |

Development begins November 4 unless earlier coding permission is documented. Selection is announced October 27; it is not a development-start date.

## UI state checklist

Planning: map lobby, seat readiness, aiming, in-flight/return, hit/miss/pending, disconnect/resume, ballot, reveal, replay, Court and operator states. Use a screen/state document first; high-fidelity mockups are not a gate to coding.

Graybox: actual camera, readable target, aim/power/spin and visible confirmed versus provisional results. Get one meaningful playtest before art polish.

Core flow: coherent low-poly assets, participant-safe identities, clear vote timer and accessible text/contrast. Distinguish seat colors with names/symbols as well as color.

Evidence and faults: factual/alternate Court views labeled, inconclusive state, pending background results, replay verification failure, reconnect timeout and restricted operator controls.

Final: readable at presentation distance, sound/mute behavior, no debug leaks, no live asset downloads.

## Cuts and protected scope

Cut first: LLM dialogue, extra cameras/emotes, crash resurrection, advanced tumbling/lift, elaborate bot motor models and extra art. Simplify physical models before weakening reproducibility. Bounded rollback is planned; reducing or removing it requires an explicit product/ADR update because it is in the proposal.

Never cut: deterministic core, authority, air sensing, bot clients assigned through RabbitMQ, spotting, truthful replays/Court claims, offline kit and RabbitMQ outside the tick.

## Demonstration plan

Aim for an 8-minute demonstration plus 2-minute buffer/Q&A, adjusted to organizer allocation. Show one bout excerpt, spotting/reveal, air-sensing comparison, bot budget, a brief service interruption, Court and verified replay. Choose stable fixtures for evidence; label them as fixtures. Private LAN is primary; one-machine local sessions, verified replay and a recorded video are fallback options. Remote VPS is useful only when venue connectivity is available.
