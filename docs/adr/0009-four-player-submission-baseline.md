# Four-player submission baseline and repository cleanup

Status: accepted October 21, 2026. The owner selected multiple online racers and approved a four-player proposal, then requested repository renaming and removal of the old product documents for submission.

## Decision

Four humans race in one private online room, each with an independent camera. Physical ramming, shared rules and immutable cargo ownership apply to every racer. Reject a fifth seat. Local split-screen and the offline fallback remain two-player. ADRs 0007-0008 are superseded wherever they describe two-player online or optional four-player support.

Online task #49 delivers all four seats; #67 validates two isolated four-seat rooms; #60 measures that workload with background analysis active. Former stretch task #64 is redundant and is retired as not planned. Keep public admission at one room until measured capacity permits more. No performance claim is made by expanding the target.

Rename the repository to one-trip-lang, remove obsolete product documents from the current tree, and close obsolete issues/milestones and the old cooperative PR. Preserve Git history and closed records. Publish the active planning branch to main so the submitted repository link opens the current plan.

## Consequences

Four-player collision readability, bandwidth and full-world reconciliation need explicit validation. Add a four-person online playtest alongside early two-person local sessions. Do not reduce the promised online player count silently; record and review any future scope change. Competition implementation remains planned for November 4-27, and proposal submission is recorded only after owner confirmation.
