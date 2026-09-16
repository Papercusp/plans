---
title: Recurring Inbox bulk-resolve sweep — scheduled runs so attention debt stops re-accumulating silently
slug: inbox-resolve-recurring-sweep-2026-09-01
status: draft
---

## Background
Inbox bulk-resolve (POST /api/admin/attention-bulk-resolve, op:'start') seeds a run over the attention backlog; the standing workspace bulk-automation policy decides what auto-applies vs lands in owner review. Before 2026-09-01 runs only happened when someone fired the pane by hand — the previous run went stale in review for 8 days with 144 items . Sibling cadence: plan-cleanup-recurring-sweep-2026-09-01.

## Phase 1 — per-run procedure
- **P-001** `todo` Check no inbox-resolve run is already active/in-review with pending work (harness_shared.attention_bulk_runs); if one is stuck in review >7d, nudge the owner instead of stacking a new run. Otherwise fire: POST http://127.0.0.1:3070/api/admin/attention-bulk-resolve with {op:'start',...} (the route's preflight validates the launch profile).
- **P-002** `todo` When the run settles into phase='review': census the residue by recommendation_kind/confidence (attention_bulk_run_items) and send the owner a digest via coord:send to ['human'] — adjudication is the owner's; never self-adjudicate review items.
- **P-003** `todo` Close the loop: record run id + auto-resolved/review counts (work-item comment or observation) so the inbox-bulk-resolve-health scorecard can grade cadence + drain trend across runs.
## Decisions
