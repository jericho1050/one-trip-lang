# Issue tracker

Use GitHub Issues in jericho1050/tsinelas-arena. Use gh CLI with explicit --repo when outside the checkout. The PRD issue links to the versioned PRD; the epic contains task parents; each task contains native GitHub sub-issues and a checklist. Sub-issues contain dependencies and one observable acceptance scenario.

Use structured JSON payload files or --body-file for multiline content. Read before changing an issue. Avoid duplicates by consulting docs/one-trip-lang/tracking.md. Do not close parent tasks until every required child has evidence. Do not auto-close the PRD or epic during decomposition.

Milestones are delivery gates, not effort estimates. GitHub blocked-by relationships and the textual Blocked by section must agree. Update both when a dependency changes.

Active product issues carry product:one-trip-lang and OTL-prefixed milestones. Prior Tsinelas issues remain historical; do not implement them by default or close them as completed.
