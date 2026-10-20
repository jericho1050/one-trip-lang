# Triage labels

Canonical roles map to identical GitHub labels: needs-triage, needs-info, ready-for-agent, ready-for-human, wontfix.

Type labels: type:prd, type:epic, type:task, type:subtask.
Work mode: mode:afk for specified, independently verifiable work; mode:hitl for human decisions, usability review or demonstration.
Priority: priority:core or priority:stretch. status:blocked means an explicit prerequisite is unresolved.

Initial issues use needs-triage. Remove that label when triaged. Apply ready-for-agent only after dependencies and the development-start gate are satisfied. AFK describes the work, not permission to start or merge.
