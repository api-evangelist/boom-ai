---
name: Ingest people and behavioral events into Boom
description: Upsert customers and record the behavioral events that trigger Boom journeys, idempotently and in bulk.
api: openapi/boom-ai-openapi-original.json
operations:
  - cdp_people_upsert
  - cdp_people_batch_upsert
  - cdp_people_get
  - cdp_events_record
  - cdp_events_batch_record
  - cdp_custom_objects_upsert
---

# Ingest people and behavioral events

Use this to load and keep Boom's CDP in sync so agents and journeys have accurate customer data.

## Auth
Send `Authorization: Bearer boom_org_...` (organization API key) on every request. Rehearse against `https://dev.useboom.ai` with a development-organization key before hitting production `https://www.useboom.ai`.

## Steps
1. **Upsert a person** with `cdp_people_upsert` — key on your own stable `externalId`. Re-sending the same `externalId` updates in place (free-form attributes are fully replaced), so it is safe to retry.
2. **Bulk load** with `cdp_people_batch_upsert` — up to 1000 people per request; documented as idempotent and safely retryable. Use this for historical/initial loads.
3. **Attach domain records** with `cdp_custom_objects_upsert` (the object's type must already exist — create it first with `cdp_custom_object_types_create`).
4. **Record a real-time event** with `cdp_events_record` — this is the path that triggers journey enrollment. Key on the event's `externalId`; re-recording returns `created: false`.
5. **Bulk/historical events** go through `cdp_events_batch_record` (up to 1000) — note this does NOT trigger journey enrollment.
6. **Read back** with `cdp_people_get` by `externalId` to confirm state.

## Conventions
- Idempotency is via `externalId`, not an Idempotency-Key header (see conventions/boom-ai-conventions.yml).
- Respect the 1,000 requests/minute limit — on `429`, honor `Retry-After` and prefer the `/batch` endpoints.
- Errors return `{ "error": { "code", "message" } }` (see errors/boom-ai-error-codes.yml).
