---
title: Alert on new critical-severity work items in papercusp
slug: critical-severity-alert-2026-07-06
status: draft
---

## Background
Owner ask (verbatim, 2026-07-06): "I want to be alerted whenever a new critical-severity work item appears in this harness." Baseline check (2026-07-06T22:15Z): zero open bug/change/task items in papercusp currently carry severity=critical (highest open severities seen were major/minor), so the fact was seeded to "now" rather than backfilling an alert for pre-existing items.

## Decisions
- D-001: No existing event-driven mechanism fires on work-item creation filtered by severity — a 5-min poll+diff was built instead of forcing `watch:create` onto a nonexistent pattern. If/when the platform grows a `work_item:created` event key, this plan should switch to `watch:create` on it and drop the poll.
- D-002: Alert delivery = `coord:send { to:['human'] }`, matching the daily-digest plan's precedent (no email transport in this workspace).
