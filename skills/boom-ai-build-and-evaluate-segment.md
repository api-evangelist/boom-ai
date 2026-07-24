---
name: Build, validate, and evaluate a Boom segment
description: Author a customer segment, validate and preview it, then evaluate it and read its members.
api: openapi/boom-ai-openapi-original.json
operations:
  - segments_catalog
  - segments_validate
  - segments_preview
  - segments_create
  - segments_evaluate
  - segments_members_list
---

# Build and evaluate a segment

Use this to define an audience Boom can target with initiatives and journeys.

## Auth
`Authorization: Bearer boom_org_...`. Rehearse on `https://dev.useboom.ai` first.

## Steps
1. **Discover selectable fields** with `segments_catalog` — the person/computed attributes and custom object types you can filter on.
2. **Validate** your definition with `segments_validate` before saving.
3. **Preview** the matched size/sample with `segments_preview` to sanity-check the rule.
4. **Create** the segment with `segments_create` (addressed by `slug`).
5. **Evaluate** with `segments_evaluate` to (re)compute membership.
6. **Read members** with `segments_members_list` (cursor-paginated, newest first).

## Conventions
- Segments are addressed by `slug`; list/member reads use `cursor` + `limit` → `data` + `next_cursor`.
- Errors return `{ "error": { "code", "message" } }`; `422` means the definition is well-formed but semantically invalid.
