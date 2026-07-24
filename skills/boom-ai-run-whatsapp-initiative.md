---
name: Create and launch a WhatsApp initiative
description: Stand up a Boom outreach initiative, link an approved WhatsApp template, launch it, add participants, and read the conversation results.
api: openapi/boom-ai-openapi-original.json
operations:
  - initiatives_create
  - initiatives_templates_set
  - initiatives_launch
  - initiatives_participants_add
  - initiatives_participant_messages_list
  - initiatives_summary
  - initiatives_participants_stop
---

# Create and launch a WhatsApp initiative

Use this to run an automated outbound WhatsApp campaign (collections, churn recovery, onboarding, research) end to end.

## Auth
`Authorization: Bearer boom_org_...`. Launching and adding participants require an org admin. **These actions send real WhatsApp messages to real customers — rehearse on `https://dev.useboom.ai` first.**

## Steps
1. **Create a draft** with `initiatives_create` — only a `name` is required.
2. **Link the round-1 template** with `initiatives_templates_set` — a WhatsApp initiative cannot launch until round 1 has an approved template linked.
3. **Launch** with `initiatives_launch` — the initiative goes active and Boom starts reaching out (org admin required).
4. **Add participants** with `initiatives_participants_add` — each person added receives a real outbound WhatsApp message; Do-Not-Contact people are skipped.
5. **Monitor** with `initiatives_summary` (participant count + per-variable coverage) and `initiatives_participant_messages_list` (full transcript per participant).
6. **Stop a participant** with `initiatives_participants_stop` if needed — idempotent and safe; it never sends, and their answers/transcript stay readable.

## Conventions
- List endpoints are cursor-paginated (`cursor` + `limit` → `data` + `next_cursor`).
- `409` means wrong lifecycle state (e.g. editing a non-draft); `429` means back off per `Retry-After`.
