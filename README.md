# One Trip Lang

A competitive 3D browser game about racing overloaded grocery trolleys home in one trip. Preserve your 100 grocery points and beat the shared deadline. Points determine the winner; time breaks a tie.

Current direction: **One Trip Lang**, approved October 21, 2026. The repository retains its historical `tsinelas-arena` slug. Earlier Tsinelas documents/issues remain historical and are not the current implementation backlog.

## Start here

- [Product requirements](docs/one-trip-lang/PRD.md)
- [Technical implementation plan](docs/one-trip-lang/technical-plan.md)
- [Milestones and UI fidelity](docs/one-trip-lang/roadmap.md)
- [Assets and presentation](docs/one-trip-lang/assets.md)
- [Current GitHub epic and task index](docs/one-trip-lang/tracking.md)
- [Competitive pivot decision](docs/adr/0007-one-trip-lang-competitive-pivot.md)

## Status and scope

A local two-player split-screen design prototype exists outside this production repository. Production networking, replay verification, Cargo Lab and infrastructure are planned, not implemented. Proposal submission and selection are unconfirmed.

Core: two humans, one route, physical cargo, fair start, score loss, deadline, authoritative online results and rematch. Four online players are stretch. No trolley ramming or manual packing in v1.

Development window: November 4-27; presentation November 29, 2026, Asia/Manila. Pre-development prototype eligibility remains a tracked organizer question. Solo, agent-assisted effort; dates are target gates rather than effort guarantees.

RabbitMQ carries background results/replay/analysis. It never sits between player input and simulation. One shared simulation supports authority, replay and Cargo Lab. Minimal K3s/IaC demonstrates repeatable deployment and isolated worker recovery, with Compose as the offline fallback.
