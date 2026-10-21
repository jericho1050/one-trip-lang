# One Trip Lang domain context

Current product: competitive grocery trolley racing. See ADR 0007 and docs/one-trip-lang/. Historical Tsinelas vocabulary is superseded for active work.

- **Race:** one shared countdown, active clock, finish/deadline resolution and results.
- **Player / seat:** one human and one independent trolley. Two-player online is core; four is stretch.
- **Load:** six versioned groceries in an identical preset for each player.
- **Grocery points:** 100 initially, assigned per item; loss is irreversible during a race.
- **Spill / loss:** forbidden ground contact, out-of-bounds loss or absence from the finish delivery volume. Deduct each item's value at most once.
- **Gate:** ordered mandatory course trigger before the finish can qualify.
- **Finisher:** crosses a valid finish before the deadline; points then finish tick determine placing.
- **DNF:** no valid finish before the deadline, or disconnect grace expired. Ranked below all finishers; all-DNF has no winner.
- **Ghost contact:** visual overlap with a rival, without physical interaction between their trolley/cargo and yours.
- **Authority:** server process that advances the only official clock and race outcomes.
- **Replay:** versioned initial state, accepted controls, hashes and events sufficient to verify a race.
- **Cargo Lab:** bounded post-race experiment changing specified brake controls. Never changes official results or claims a global optimum.
- **Outbox:** durable records awaiting asynchronous publication; not an instruction to await I/O inside the simulation tick.
- **Local prototype:** pre-development design experiment; not production network or determinism evidence.

Owner: repository owner. Language: English with Filipino game terms. Dates: Asia/Manila. Estimates are targets pending measurement.
