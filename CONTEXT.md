# One Trip Lang domain context

Current product: competitive grocery trolley racing. See ADRs 0007-0009 and docs/one-trip-lang/. Four online players and a two-player local fallback are the current scope.

- **Race:** one shared countdown, active clock, finish/deadline resolution and results.
- **Player / seat:** one human and one independent trolley. Four-player online is core; local split-screen remains two-player.
- **Load:** six versioned groceries in an identical preset for each player.
- **Grocery points:** 100 initially, assigned per item; loss is irreversible during a race.
- **Spill / loss:** forbidden ground contact, out-of-bounds loss or absence from the finish delivery volume. Deduct each item's value at most once.
- **Gate:** ordered mandatory course trigger before the finish can qualify.
- **Finisher:** crosses a valid finish before the deadline; points then finish tick determine placing.
- **DNF:** no valid finish before the deadline, or disconnect grace expired. Ranked below all finishers; all-DNF has no winner.
- **Ram:** physical trolley contact that can disturb either load; contact itself never deducts points.
- **Room:** private join-code session with four seats, one isolated physics world and its own race lifecycle. Rematches get new match IDs inside the room.
- **Server:** a process hosting a bounded number of rooms; a VPS hosts that process and background services. Rooms share CPU capacity but never gameplay state.
- **Prediction:** temporary client simulation of the interacting world; authoritative corrections replace it.
- **Cleared racer:** finished or DNF trolley/cargo removed from live collisions; its result remains recorded.
- **Authority:** server process that advances the only official clock and race outcomes.
- **Replay:** versioned initial state, accepted controls, hashes and events sufficient to verify a race.
- **Cargo Lab:** bounded post-race whole-world experiment changing one player’s specified brake controls while holding opponents’ recorded controls fixed. Never changes official results or claims a global optimum.
- **Outbox:** durable records awaiting asynchronous publication; not an instruction to await I/O inside the simulation tick.
- **Local prototype:** pre-development design experiment; not production network or determinism evidence.

Owner: repository owner. Language: English with Filipino game terms. Dates: Asia/Manila. Estimates are targets pending measurement.
