# Papercusp — shared plan templates

Public mirror repo backing the **Plans** tab of the Papercusp Cupboard.

Each subdirectory is one self-describing plan template (`plan.md` + `listing.json`),
published by `cupboard:publish-plan` and installed by `cupboard:install-plan`.
Templates are sanitized before export: item statuses are reset to `todo`, and
set-status notes, work-item ids, the `## Now` block and identity frontmatter are
stripped. The goal, item DAG, decisions and prose are kept.

Install one into your own workspace:

    cupboard:install-plan { listingId: "<listing ref>" }

| template | what it does |
|---|---|
| `gmail-respond-with-draft-2026-08-22` | Respond to an inbound Gmail message with a prepared draft |
| `meeting-prep-brief-2026-08-22` | Prepare a brief for an upcoming Calendar meeting |
| `plan-cleanup-recurring-sweep-2026-09-01` | Scheduled sweep so stale-plan debt becomes a measurable trend |
| `inbox-resolve-recurring-sweep-2026-09-01` | Scheduled Inbox bulk-resolve so attention debt stops re-accumulating |
| `critical-severity-alert-2026-07-06` | Alert routing for critical-severity events |
