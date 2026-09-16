---
title: Gmail message — respond with a draft
slug: gmail-respond-with-draft-2026-08-22
status: draft
---

# Gmail message — respond with a draft

## Background

The trigger run carries the normalized email under `plan_run.inputs.trigger.payload`.
The draft tool accepts only that run's numeric id; it resolves the recipient, thread,
reply headers, and OAuth credential server-side. It creates a Gmail DRAFT and never sends.

## Phase 1 — Draft

- **P-001** `todo` Read `payload.plan_run.inputs.trigger.payload`, compose a concise response, then call `gmail:create-draft` with `planRunId=payload.plan_run.runId` and the response text. Complete only after the tool reports `created:true` or `alreadyCreated:true`.
## Decisions

### D-001 — Draft creation is anchored to a trigger plan run; auto-send stays outside this tool
Date: 2026-08-22
The tool resolves every Gmail coordinate and credential from the durable trigger run. Its public input is only planRunId plus text. It has no send branch; automatic sending is a separate owner-authority dark-flag surface.
