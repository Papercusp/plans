---
title: Recurring plan-cleanup sweep — scheduled scanner runs so stale-plan debt becomes a measurable trend
slug: plan-cleanup-recurring-sweep-2026-09-01
status: draft
---

## Background
Plan-cleanup (the Plans-pane scanner, `POST /api/admin/plan-cleanup`) finds stale `## Now` sections, cleared blockers, flip-to-done candidates, archive candidates. Until 2026-09-01 it had run exactly once — no cadence, so convergence was ungradable (scorecard). This plan exists to hang the recurrence on; the schedule is authored via plans:set-schedule and armed via plans:arm-schedule. Related but distinct: cleanup-report-flows-2026-08-24 (the shipped feature plan that built the scanner) and plan-cleanup-health (the grading rubric).

## Phase 1 — per-run procedure
- **P-001** `todo` Enumerate candidate plans (plans:list — status active/ready, not archived) and fire the scanner: POST http://127.0.0.1:3070/api/admin/plan-cleanup with {op:'start', planSlugs:[...]}. The deterministic pass runs to a fixed point first; a resolver is launched only when judgment residue remains.
- **P-002** `todo` When the run reaches phase='review': for provable findings whose target you can re-verify live, apply the canonical mutation (plans:set-status etc.) then record acceptance via the run's recheck seam (op:'recheck-finding'). Judgment kinds (stale-now, flip-to-done, semantic) go to the owner via coord:send to ['human'] — never self-adjudicate those.
- **P-003** `todo` Close the loop: note run id + accepted/dismissed/remaining counts (a work-item comment or observation) so the next plan-cleanup-health scorecard can grade the across-runs trend.
## Decisions
