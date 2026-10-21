# Agent instructions

Read CONTEXT.md, docs/one-trip-lang/PRD.md, docs/one-trip-lang/technical-plan.md and ADRs 0007-0009 before implementation. ADR 0009 sets four-player online scope. Removed product plans remain recoverable in Git history. These documents describe planned production behavior, not existing production code.

## Working rules

- Competition implementation is scheduled for November 4, 2026. The user explicitly authorized separate local design prototypes on October 21; do not claim organizer approval or eligibility from that authorization. Record prework policy in the active rules issue.
- Preserve the never-cut requirements. Defer stretch work until the core demo passes.
- One focused issue per branch/PR. Respect declared dependencies; check their actual acceptance evidence, not just their closed status.
- Use the shared simulation for every authoritative outcome. No duplicate physics implementation inside React components or analysis code.
- Never block a simulation tick on RabbitMQ, a database, remote AI or HTTP. Resource limits and recovery must be explicit.
- The server owns race clock, item-loss transitions, finish validation and ranking. Clients submit controls, never their own outcomes. Rival trolley/cargo collisions are core. Preserve physical wobble, immutable cargo ownership, separate room worlds and collision-aware replay under ADR 0008.
- Use available libraries for rendering, collision, storage and transport. Our custom engineering belongs in simulation rules, networking integration, Cargo Lab and replay evidence.
- Test external behavior. Require replay, determinism, networking and failure-recovery evidence; do not add tests that simply mirror presentation code.
- Work on isolated branches. Do not merge your own changes or publish externally unless the current task authorizes it. Documentation changes and issue creation are already authorized for initial planning.
- New dependencies need an explanation of the work they remove. Minimal K3s and IaC are approved planning scope under ADR 0007. No service mesh, unbounded workers or runtime LLM dependency. Gameplay gates come first.
- Use assets with recorded source and license. No hand-modeling requirement. Never commit API keys or downloaded assets with unknown rights.
- Estimates are planning targets, not benchmarks. Label measured results with build/version, hardware and test conditions.
- Do not spawn subagents by default; follow explicit user authorization for delegation.

## Agent skills

### Issue tracker

GitHub Issues tracks the PRD, epic, tasks and sub-issues. See docs/agents/issue-tracker.md.

### Triage labels

Use the canonical triage label names plus type, priority and work-mode labels. See docs/agents/triage-labels.md.

### Domain docs

Single-context layout: CONTEXT.md and docs/adr/. See docs/agents/domain.md.
