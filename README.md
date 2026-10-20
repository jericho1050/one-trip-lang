# Tsinelas Arena

A four-seat 3D browser game: squash an air-sensing cockroach, identify hidden bots, and take your lag excuse to Slipper Court.

PandesalDEV Wackathon 2026: **Useless Problems. Serious Engineering.**

## Status

Planning only. There is no playable implementation yet. Proposal prepared; submission and selection are not confirmed here. Development is scheduled for November 4-27, with the live demo November 29, 2026. Dates use Asia/Manila.

Solo, agent-assisted development. We use observable integration gates rather than assumed person-days. Repository visibility is private; change it if organizer submission rules require public access.

## Start here

- [PRD and business rationale](docs/PRD.md)
- [Technical plan](docs/technical-plan.md)
- [Asset plan and inventory](docs/assets.md)
- [Milestones and UI fidelity gates](docs/roadmap.md)
- [GitHub tracking index](docs/planning/tracking.md)
- [Domain language](CONTEXT.md) and [architecture decisions](docs/adr/)
- [Agent working instructions](AGENTS.md)

## Product boundaries

One room, four fixed throwing stations, desktop browsers, one cockroach. One or two seats are hidden bots, fixed during each bout. One shared deterministic simulation powers playback, bot planning, bounded rollback and Court experiments. RabbitMQ stays outside the gameplay tick.

Never cut: determinism, authoritative outcomes, the air-sensing cockroach, bots as clients assigned through RabbitMQ, bot spotting, truthful replays, the offline demo and the broker boundary.

Use GitHub Issues for work tracking. Complete tasks through linked pull requests with evidence for their acceptance test. No implementation before November 4 unless organizer permission is recorded.
