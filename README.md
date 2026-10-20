# Tsinelas Arena

A four-seat cooperative 3D browser game: work together to squash an air-sensing cockroach, then guess which teammates were bots. Slipper Court is an optional-to-open evidence feature for controlled lag complaints.

PandesalDEV Wackathon 2026: **Useless Problems. Serious Engineering.**

## Status

Planning only. There is no playable implementation yet. Proposal prepared; submission and selection are not confirmed here. Development is scheduled for November 4-27, with the live demo November 29, 2026. Dates use Asia/Manila.

Solo, agent-assisted development. We use observable integration gates rather than assumed person-days. Repository visibility is private; change it if organizer submission rules require public access.

## Start here

- [Delivery epic #2](https://github.com/jericho1050/tsinelas-arena/issues/2) and [dated milestones](https://github.com/jericho1050/tsinelas-arena/milestones)
- [PRD and business rationale](docs/PRD.md)
- [Technical plan](docs/technical-plan.md)
- [Asset plan and inventory](docs/assets.md)
- [Milestones and UI fidelity gates](docs/roadmap.md)
- [GitHub tracking index](docs/planning/tracking.md)
- [Domain language](CONTEXT.md) and [architecture decisions](docs/adr/)
- [Agent working instructions](AGENTS.md)

## Product boundaries

One team, one room, four fixed throwing stations, desktop browsers, one cockroach. Humans and bots help the same team; there is no sabotage or elimination. Every finalized squash adds to the shared team score. One or two seats are hidden bots, fixed during each bout. One shared deterministic simulation powers playback, bot planning, bounded rollback and Court experiments. RabbitMQ stays outside the gameplay tick.

Never cut: determinism, authoritative outcomes, the air-sensing cockroach, bots as clients assigned through RabbitMQ, bot spotting, truthful replays, the offline demo and the broker boundary.

Use GitHub Issues for work tracking. Complete tasks through linked pull requests with evidence for their acceptance test. No implementation before November 4 unless organizer permission is recorded.

## Next actions

Start with the planning task's rules/status record and licensed asset shortlist. These are the only currently unblocked planning slices. At the permitted development start, the first implementation slice is one playable graybox throw. Do not begin with infrastructure expansion or polished art.

Task checklists show delivery progress; native sub-issue links show hierarchy; native blocked-by relationships show ordering. Labels distinguish agent-ready work from work requiring a human, but all initial issues still require triage.
