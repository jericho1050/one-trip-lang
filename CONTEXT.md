# Domain context

- **Team:** all four seats, humans and bots together, cooperate to squash the cockroach. Bot identity is hidden; bot intent is helpful. No sabotage, impostor victory condition or elimination.
- **Team score:** one shared point per finalized squash, regardless of which seat lands the throw.
- **Seat:** one of four fixed throwing stations; controlled by a human or bot for an entire bout.
- **Bout:** 90-second active phase followed by a 15-second spotting ballot and reveal. These durations are initial tuning defaults.
- **Match:** one bout in v1. No tournament or multi-bout progression.
- **Throw:** a legal launch defined by quantized direction, power and spin, admitted by the authoritative server.
- **Slipper:** one active projectile per seat. After flight ends, it returns automatically; no fetching mechanic.
- **Ipis:** the shared cockroach. Its escape decisions are recorded as actor inputs, informally called player 5; it is not a network seat.
- **Finalized:** older than the rollback window and committed by the authority; cannot be changed by late input or Court.
- **Spotting:** one bot/human/abstain classification per teammate, hidden until ballot close. Personal spotting points are separate from the shared team score.
- **Bot budget:** number of candidate flights simulated for a planning attempt, with a separate wall-clock deadline. It is not an LLM token budget.
- **Understudy:** a bot client hosted alongside the server that takes an unclaimed bot seat, still using the public gameplay connection and protocol.
- **Slipper Court:** an experimental replay changing only the deliberate delay applied to the claimant's recorded input stream. It reports conditional outcomes, never diagnoses unknown network lag.
- **Public state:** information available equally to human and bot clients. Excludes hidden roles, server secrets and future cockroach choices.
- **Simulation hash:** a hash of canonical authoritative simulation state at a specified finalized tick and simulation version. Predicted states at different ticks are not comparable.
- **Air field:** simplified orientation-dependent disturbance, not computational fluid dynamics or a validated biological simulator.

Product owner and final scope approver: the repository owner. Working language: English with Filipino game terms.
