---
title: Meeting prep brief — granted Personal Vault consumer
slug: meeting-prep-brief-2026-08-22
status: draft
---

# Meeting prep brief

## Background

Prepare a concise, private pre-meeting brief from the normalized Calendar trigger and explicitly granted Personal Vault context. Personal data is optional and default-deny: a refusal is silent, never an error and never evidence that private data exists.

## Phase 1 — prepare and deliver the brief

- **P-001** `todo` Parse the server-supplied trigger input; extract meeting title, time, description/agenda, attachment references, and attendee names/emails. Never accept a prompt-authored principal or scope override.
- **P-002** `todo` Query personal:search for recent attendee threads and prior meeting context using participants plus scopes personal:gmail, personal:calendar, and personal:contacts; bound snippets/results, preserve provenance, and continue with trigger-only context when authorization refuses or returns no results. blocked-by: P-001
- **P-003** `todo` Synthesize a concise brief with meeting facts, attendee context, open threads, agenda, and source provenance; exclude any category not returned by the authorized search. blocked-by: P-002
- **P-004** `todo` Deliver the brief through both owner surfaces with `notifications:send_owner`: use one stable `dedupeKey` derived from `trigger.dedupeKey` plus this launched plan-run ref, pass the Calendar event as `sourceRef`, and record the returned `inbox.msgId` plus `attention.recordId` as delivery evidence. blocked-by: P-003
## Decisions

### D-001 — Private context is optional and default-deny
Date: 2026-08-22
The trigger payload is the only mandatory source. Personal Vault context is admitted only by the server-side plan-template grant resolver; coding roles and ungranted runs receive no block, no heading, and no existence signal.
