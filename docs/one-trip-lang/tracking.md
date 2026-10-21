# One Trip Lang - GitHub Tracking

Repository: https://github.com/jericho1050/tsinelas-arena
Active filter: [One Trip Lang issues](https://github.com/jericho1050/tsinelas-arena/issues?q=is%3Aissue+label%3Aproduct%3Aone-trip-lang)

- [PRD](https://github.com/jericho1050/tsinelas-arena/issues/34)
- [Delivery epic](https://github.com/jericho1050/tsinelas-arena/issues/35)

Old Tsinelas issues are preserved as historical planning; this index is the active backlog. All new issues begin needs-triage, not completed. Native parent-child and blocker links match the textual graph.

## Milestones

- [OTL M0 - Proposal and product baseline](https://github.com/jericho1050/tsinelas-arena/milestone/7) - 2026-10-21: Current proposal and PRD prepared; submission and prototype-eligibility status recorded by the owner.
- [OTL M1 - Playable local race](https://github.com/jericho1050/tsinelas-arena/milestone/8) - 2026-11-07: Production simulation supports two local racers, physical wobble/ramming, fair scoring, rematch and whole-match replay fixtures.
- [OTL M2 - Two-player online race](https://github.com/jericho1050/tsinelas-arena/milestone/9) - 2026-11-12: Two-browser collision races and two isolated rooms pass lifecycle tests; human playtests guide tuning.
- [OTL M3 - Evidence and useful analysis](https://github.com/jericho1050/tsinelas-arena/milestone/10) - 2026-11-18: Verified replay, truthful brake experiment and broker/worker recovery are demonstrated.
- [OTL M4 - Hosted and recognizable](https://github.com/jericho1050/tsinelas-arena/milestone/11) - 2026-11-23: Repeatable K3s deployment, bounded workers and readable licensed assets run together.
- [OTL M5 - Release frozen](https://github.com/jericho1050/tsinelas-arena/milestone/12) - 2026-11-27: Measured quality gates, offline kit and three rehearsals pass; release frozen.
- [OTL M6 - Live presentation](https://github.com/jericho1050/tsinelas-arena/milestone/13) - 2026-11-29: Frozen entry and fallback are presented; demo and Q&A outcomes recorded.

## [Proposal, rules and asset readiness](https://github.com/jericho1050/tsinelas-arena/issues/36)

- [P1: Refresh the proposal for the competitive grocery race](https://github.com/jericho1050/tsinelas-arena/issues/43) - HITL, core; blocked by none.
- [P2: Record development eligibility and the production start gate](https://github.com/jericho1050/tsinelas-arena/issues/44) - HITL, core; blocked by none.
- [P3: Select the minimum licensed grocery and environment assets](https://github.com/jericho1050/tsinelas-arena/issues/45) - AFK, core; blocked by none.

## [Complete a fair local grocery race](https://github.com/jericho1050/tsinelas-arena/issues/37)

- [S1: Drive one trolley through the production course](https://github.com/jericho1050/tsinelas-arena/issues/46) - AFK, core; blocked by #44.
- [S2: Complete the cargo score and deadline loop](https://github.com/jericho1050/tsinelas-arena/issues/47) - AFK, core; blocked by #46.
- [C1: Ram a rival with physical wobble and fair cargo losses](https://github.com/jericho1050/tsinelas-arena/issues/66) - AFK, core; blocked by #47.
- [S3: Play and rematch with independent local controls](https://github.com/jericho1050/tsinelas-arena/issues/48) - AFK, core; blocked by #66.

## [Race a friend in an authoritative online room](https://github.com/jericho1050/tsinelas-arena/issues/38)

- [S4: Join and finish a real two-browser race](https://github.com/jericho1050/tsinelas-arena/issues/49) - AFK, core; blocked by #48.
- [R1: Run isolated private matches on one bounded server](https://github.com/jericho1050/tsinelas-arena/issues/67) - AFK, core; blocked by #49.
- [S5: Keep racing responsive under delay and hostile input](https://github.com/jericho1050/tsinelas-arena/issues/50) - AFK, core; blocked by #49.
- [S6: Reconnect a seat without pausing the race](https://github.com/jericho1050/tsinelas-arena/issues/51) - AFK, core; blocked by #49.

## [Verify races and test useful braking alternatives](https://github.com/jericho1050/tsinelas-arena/issues/39)

- [S7: Verify a recorded race against the shared simulation](https://github.com/jericho1050/tsinelas-arena/issues/52) - AFK, core; blocked by #66.
- [S8: Publish durable results and replay work outside the tick](https://github.com/jericho1050/tsinelas-arena/issues/53) - AFK, core; blocked by #49, #52.
- [S9: Run a bounded earlier-braking Cargo Lab experiment](https://github.com/jericho1050/tsinelas-arena/issues/54) - AFK, core; blocked by #52, #53.
- [S10: Recover analysis jobs without duplicate effects](https://github.com/jericho1050/tsinelas-arena/issues/55) - AFK, core; blocked by #53, #54.

## [Host a readable game with repeatable infrastructure](https://github.com/jericho1050/tsinelas-arena/issues/40)

- [S11: Make the race readable with licensed assets and cues](https://github.com/jericho1050/tsinelas-arena/issues/56) - AFK, core; blocked by #48, #45.
- [S12: Deploy one reproducible HTTPS race environment](https://github.com/jericho1050/tsinelas-arena/issues/57) - AFK, core; blocked by #49, #53, #44.
- [S13: Protect live race resources while workers restart or scale](https://github.com/jericho1050/tsinelas-arena/issues/58) - AFK, core; blocked by #54, #55, #57.

## [Validate fun, reliability and an offline release](https://github.com/jericho1050/tsinelas-arena/issues/41)

- [S14: Playtest and tune the competitive tradeoff](https://github.com/jericho1050/tsinelas-arena/issues/59) - HITL, core; blocked by #48.
- [S15: Measure online quality and abuse boundaries](https://github.com/jericho1050/tsinelas-arena/issues/60) - AFK, core; blocked by #50, #51, #55, #56, #58, #67.
- [S16: Package a fully offline two-player fallback](https://github.com/jericho1050/tsinelas-arena/issues/61) - AFK, core; blocked by #53, #54, #56.
- [S17: Rehearse, document and freeze the release](https://github.com/jericho1050/tsinelas-arena/issues/62) - HITL, core; blocked by #59, #60, #61.

## [Deliver the live demo and optional expansion](https://github.com/jericho1050/tsinelas-arena/issues/42)

- [S18: Present the frozen entry and record the outcome](https://github.com/jericho1050/tsinelas-arena/issues/63) - HITL, core; blocked by #62.
- [X1: Stretch: expand a proven room to four humans](https://github.com/jericho1050/tsinelas-arena/issues/64) - AFK, stretch; blocked by #60, #62.

## Operating rules

Work from an unblocked leaf, read the active PRD/technical plan and attach evidence for its single acceptance scenario. Implementation checklists are steps, not separate success claims. Remove blocked labels only when dependencies have passed. Close parents after all core children pass; do not wait on optional four-player work. Keep the prototype, production implementation and human playtest evidence distinct.
