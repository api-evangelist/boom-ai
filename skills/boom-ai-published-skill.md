---
name: Boom
description: Use when building customer outreach campaigns, managing AI-driven conversations over WhatsApp, creating customer segments, designing journeys, managing customer data, or extracting structured insights from conversations. Agents should reach for this skill when users need to launch initiatives, configure journeys, manage participants, query customer data, or analyze conversation results.
metadata:
    mintlify-proj: boom
    version: "1.0"
---

# Boom AI Skill

## Product summary

Boom AI is a customer engagement platform that runs one AI agent per organization to conduct WhatsApp conversations with customers. The agent handles win-backs, support, research, onboarding, lead qualification, and document collection—all from a single knowledge base briefing. Agents work with Boom through two identical surfaces: REST API (base URL `https://www.useboom.ai/api/v1`) and MCP tools (via `https://www.useboom.ai/mcp`). Key concepts: **initiatives** (outreach missions), **journeys** (step-by-step workflows), **segments** (audience filters), **extraction** (structured data from conversations), and **CDP** (customer data platform). Authentication uses organization API keys (prefix `boom_org_`). See the full documentation at https://docs.useboom.ai.

## When to use

Reach for this skill when:
- **Building outreach campaigns**: creating initiatives, designing journeys, launching to audiences
- **Managing customer data**: upserting people, objects, events, relationships; querying the CDP
- **Defining audiences**: building segments with filters, evaluating membership, previewing counts
- **Configuring conversations**: setting extraction schemas, defining what data to pull from conversations
- **Managing participants**: adding people to initiatives, monitoring progress, stopping outreach
- **Reading results**: fetching transcripts, extracted values, aggregate summaries
- **Connecting data sources**: syncing from PostgreSQL/MySQL or pushing via API
- **Using MCP**: connecting Claude, Cursor, or other AI tools to Boom without API keys

Do not use this skill for: dashboard-only operations (email template creation, knowledge base editing, team management), authentication setup, or account provisioning.

## Quick reference

### Base URLs and authentication
| Environment | URL | Use |
|---|---|---|
| Production | `https://www.useboom.ai` | Live data, real journeys |
| Development | `https://dev.useboom.ai` | Sandbox testing |

All requests require: `Authorization: Bearer boom_org_YOUR_KEY`

### Core endpoints (REST)
| Resource | Endpoint | MCP tool |
|---|---|---|
| People | `POST /api/v1/cdp/people` | `cdp_people_upsert` |
| Events | `POST /api/v1/cdp/events` | `cdp_events_record` |
| Custom objects | `POST /api/v1/cdp/custom-objects` | `cdp_custom_objects_upsert` |
| Relationships | `POST /api/v1/cdp/relationships` | `cdp_relationships_link` |
| Segments | `POST /api/v1/segments` | `segments_create` |
| Initiatives | `POST /api/v1/initiatives` | `initiatives_create` |
| Journeys | `POST /api/v1/journeys/draft` | `journeys_create_draft` |
| Participants | `POST /api/v1/initiatives/{id}/participants` | `initiatives_participants_add` |
| Extraction | `POST /api/v1/initiatives/{id}/extraction-schema` | `extraction_schema_set` |

### Initiative lifecycle
```
DRAFT ──launch──► ACTIVE ──► COMPLETED
  │                 │
  └── editable      └── cancel, archive
```

Only drafts are editable. Launching is irreversible and sends real messages.

### Journey node types
| Node | Purpose | Key rule |
|---|---|---|
| `ENTRY` | Where people start (manual, segment, or event) | Exactly one per journey |
| `SEND_MESSAGE` | Send WhatsApp template | Template must match channel's account |
| `WAIT_FOR_REPLY` | Wait for customer response | Emits `REPLIED` or `TIMEOUT` |
| `MANAGE_CONVERSATION` | Run AI conversation or escalate | Emits `CLOSED` or `STALE` |
| `DECISION` | Two-way branch (AND/OR logic) | Both `YES` and `NO` must wire |
| `CASE` | Multi-way switch on attribute | All branches + default must wire |
| `DELAY` | Pause for duration or until date | Pure wait, doesn't race replies |
| `DISPATCH_EVENT` | Record CDP event | Enrolls person into another journey |
| `EXIT` | End journey for person | At least one required |

### Segment filter operators
| Type | Operators |
|---|---|
| STRING | `eq`, `neq`, `in`, `not_in`, `contains`, `not_contains`, `starts_with`, `ends_with`, `is_null`, `is_not_null` |
| NUMBER | `eq`, `neq`, `gt`, `gte`, `lt`, `lte`, `in`, `not_in`, `is_null`, `is_not_null` |
| DATE | `in_last_n`, `in_next_n`, `more_than_n_ago`, `before`, `after`, `between` |

### Extraction field types
| Type | Use for |
|---|---|
| `bool` | Binary yes/no flags |
| `int` | Whole numbers, optionally bounded |
| `enum` | Single value from fixed list |
| `enum[]` | Multiple values from fixed list |
| `string` | Free text, optionally capped |
| `string[]` | Open-ended text items |

## Decision guidance

### When to use REST API vs MCP
| Scenario | Use |
|---|---|
| Server-to-server integration, scripts, scheduled jobs | REST API with organization API key |
| AI agent (Claude, Cursor) building campaigns conversationally | MCP (no API key, sign in once) |
| Existing system integration, webhooks, custom tooling | REST API |
| Rapid prototyping, exploration, learning | MCP with Claude Code |

### When to push data vs sync from database
| Scenario | Use |
|---|---|
| Real-time events, behavioral signals, one-off updates | Push via API (`cdp_people_upsert`, `cdp_events_record`) |
| Large customer base, historical data, read-only source | Database sync (PostgreSQL/MySQL) |
| Hybrid: people and objects from DB, events from API | Both (sync handles people/objects, API handles events) |

### When to use segment trigger vs manual enrollment
| Scenario | Use |
|---|---|
| Recurring campaigns, audience changes over time | Segment trigger (auto-enrolls new members) |
| One-time outreach, hand-picked list, testing | Manual enrollment (CSV or API) |
| Event-driven (payment made, signup, etc.) | CDP event trigger |

### When to set extraction schema
| Scenario | Action |
|---|---|
| Before launch | Set schema (required; conversations extract against current schema) |
| After launch | Cannot re-extract closed conversations; new schema applies to future conversations only |
| Changing fields | Submit complete schema (not a diff); old conversations keep their values |

## Workflow

### 1. Set up customer data
1. Create an API key in the Boom dashboard (shown once; store securely)
2. Upsert people: `POST /api/v1/cdp/people` with `externalId`, `email`/`phoneNumber`, and `attributes`
3. Create custom object types if needed: `POST /api/v1/cdp/custom-objects/types`
4. Upsert objects: `POST /api/v1/cdp/custom-objects` with `type`, `externalId`, `attributes`
5. Register relationship types: `POST /api/v1/cdp/relationship-types` with `kind`, `role`, `customObjectType`, `cardinality`
6. Link records: `POST /api/v1/cdp/relationships` with `personExternalId`, `customObjectExternalId`, `relationshipTypeId`
7. Record events: `POST /api/v1/cdp/events` with `name`, `externalId`, subject (person or object), `properties`

### 2. Define your audience
1. Call `GET /api/v1/segments/catalog` to discover filterable attributes
2. Validate filter: `POST /api/v1/segments/validate` with `filterExpression`
3. Preview count: `POST /api/v1/segments/preview` (returns match count, no sample)
4. Create segment: `POST /api/v1/segments` with `name`, `slug`, `filterExpression`, `evaluationCadence`
5. Evaluate: `POST /api/v1/segments/{slug}/evaluate` (runs filter, writes membership)
6. List members: `GET /api/v1/segments/{slug}/members` (paginated)

### 3. Create and configure an initiative
1. Create draft: `POST /api/v1/initiatives` with `name`, `objective`, `context`, `guidingQuestions[]`
2. Set extraction schema: `POST /api/v1/initiatives/{id}/extraction-schema` with field definitions
3. Link WhatsApp template: `POST /api/v1/initiatives/{id}/templates` with template ID and round number
4. Build journey (see step 4 below)
5. Validate before launch: check that journey is published, template is approved, required fields are set

### 4. Design and publish a journey
1. Discover nodes: `GET /api/v1/journeys/authoring-catalog` (returns available node types, rules, catalogs)
2. Create draft: `POST /api/v1/journeys/draft` with `initiativeId`, definition (name, nodes, edges)
3. Add nodes: `POST /api/v1/journeys/nodes` with node kind, inputs, position
4. Connect nodes: `POST /api/v1/journeys/edges` with source node, output handle, target node
5. Set trigger: `POST /api/v1/journeys/trigger` with `triggerType` (manual, segment, cdp_event), optional frequency cap
6. Validate: `POST /api/v1/journeys/validate` (dry-run, returns issues without saving)
7. Publish: `POST /api/v1/journeys/publish` with `confirm: true` (irreversible, starts real outreach)

### 5. Launch and manage
1. **Launch before enrolling**: `POST /api/v1/initiatives/{id}/launch` (publishes journey, goes active)
2. Add test participant: `POST /api/v1/initiatives/{id}/participants` with one contact, verify message arrives
3. Add remaining participants: CSV upload in app or API batch calls
4. Monitor: `GET /api/v1/initiatives/{id}/participants` (list with status)
5. Read results: `GET /api/v1/initiatives/{id}/data/summary` (aggregate), `GET /api/v1/initiatives/{id}/participants/{id}` (per-person)
6. Stop if needed: `POST /api/v1/journeys/stop` with `confirm: true` (closes enrollment, lets conversations finish)

## Common gotchas

- **Launch before enrolling.** Adding participants requires an active initiative with a published journey. Launching with nobody enrolled is safe and sends nothing.
- **Segments need evaluation.** Creating a segment compiles the filter but doesn't evaluate it; `memberCount` is 0 until you call `segments_evaluate`. Set `evaluationCadence` to `HOURLY` or `DAILY` for time-based filters ("no payment in 30 days").
- **Extraction schema is immutable for past conversations.** Set it before launch. Changing it after launch only affects new conversations; old ones keep their extracted values.
- **Template placeholders bind differently in messages vs conditions.** In `SEND_MESSAGE` templates, use `person.<key>` for custom attributes, not `attributes.<key>`. The latter is for `DECISION`/`CASE` conditions only.
- **Segment triggers need internal ID, not slug.** The API identifies segments by `slug`, but journey triggers need the internal `segmentId`. Set segment triggers in the Boom app, not over the API.
- **Upserts are idempotent.** Running the same upsert twice returns `created: false` the second time. This is correct behavior, not an error.
- **Events are append-only.** You cannot update or delete an event. Record it once with a stable `externalId` (idempotency key).
- **Relationships require pre-registered types.** You cannot link two records without first registering the relationship type and getting its `relationshipTypeId`.
- **Do Not Contact is enforced by platform.** Suppressed contacts are skipped even if re-enrolled. This is not your code's responsibility.
- **Email send has no reply loop.** Email templates are outbound only. Only `DELAY`, `EXIT`, or non-conversational nodes can follow an email send.
- **Bulk event ingest doesn't trigger journeys.** Use the single-event endpoint for real-time, journey-triggering events. Bulk is for backfill.

## Verification checklist

Before launching an initiative:
- [ ] Initiative is in `DRAFT` status
- [ ] Extraction schema is set (if you need extracted data)
- [ ] Journey is published (status `ACTIVE`)
- [ ] WhatsApp template is approved and linked to round 1
- [ ] `objective`, `context`, and `guidingQuestions[]` are set
- [ ] Segment is evaluated (if using segment trigger) and has members
- [ ] Test participant added and message verified to arrive
- [ ] `maxAttempts` matches the number of follow-up templates you built
- [ ] Journey validates with no errors (warnings are advisory)
- [ ] All `DECISION` and `CASE` branches are wired (both `YES`/`NO`, all cases + default)
- [ ] No template placeholders reference paths that don't resolve for this trigger

After launching:
- [ ] Participants are enrolled (check `GET /api/v1/initiatives/{id}/participants`)
- [ ] Messages are sending (spot-check a few participants' message history)
- [ ] Extraction is running (check `GET /api/v1/initiatives/{id}/data/summary` for coverage)
- [ ] Conversations are closing normally (check `CLOSED` vs `STALE` counts)

## Resources

- **Full documentation**: https://docs.useboom.ai/llms.txt (comprehensive page-by-page navigation for agents)
- **API reference**: https://docs.useboom.ai/api-reference/overview (all REST endpoints and MCP tools)
- **Journeys guide**: https://docs.useboom.ai/journeys (node types, authoring, publishing, versioning)
- **Segments guide**: https://docs.useboom.ai/segments (filters, operators, evaluation cadence, membership)

---

> For additional documentation and navigation, see: https://docs.useboom.ai/llms.txt