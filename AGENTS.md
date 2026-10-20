# Agent instructions

Read CONTEXT.md, docs/PRD.md, docs/technical-plan.md and relevant ADRs before implementation. These documents describe planned behavior, not existing code.

## Working rules

- Planning only before November 4, 2026 unless organizer permission is recorded in the rules issue. Do not infer permission from the availability of AI tools.
- Preserve the never-cut requirements. Defer stretch work until the core demo passes.
- One focused issue per branch/PR. Respect declared dependencies; check their actual acceptance evidence, not just their closed status.
- Use the shared simulation for every authoritative outcome. No duplicate physics implementation inside React components or bot code.
- Never block a simulation tick on RabbitMQ, a database, remote AI or HTTP. Resource limits and recovery must be explicit.
- Bots have no privileged identity, future, seed or cockroach-brain access. Participant-visible APIs must not leak bot identities before ballots close.
- Use available libraries for rendering, collision, storage and transport. Our custom engineering belongs in simulation rules, networking integration, planning and Court evidence.
- Test external behavior. Require replay, determinism, networking and failure-recovery evidence; do not add tests that simply mirror presentation code.
- Work on isolated branches. Do not merge your own changes or publish externally unless the current task authorizes it. Documentation changes and issue creation are already authorized for initial planning.
- New dependencies need an explanation of the work they remove. Do not add Kubernetes, extra infrastructure or live LLM dependencies to the core.
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
