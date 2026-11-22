---
title: "AUTO-LTC-013, 030..037 — Housekeeping, legacy and Firbot development tooling"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make scenarios 2629639, 6477190, 4141246, 6919674, 6920671, 6920717, 6932098, 6933016, 6933260; sanitized exports"
---

# Housekeeping, legacy and Firbot development tooling

## AUTO-LTC-013 — `Delete Messages` (2629639) — active, production housekeeping

- Schedule: every 7,200 s (2 h); created 2025-08-03, last edit 2025-08-04 (oldest unchanged scenario).
- Lists **all** `LL_MessagesHistory` records, iterates and deletes records whose `Timestamp` is more than 3 h old (filter named "Message older than 4 hours" but compares `> 3`).
- Parses `Timestamp` with pattern `YYYY-MM-DD HH:mm`; the store field is now of type `date` and writers use other formats — **Inference:** age computation may be wrong for some records; verify in execution logs.
- Module labels still show the old store name `CountryMagazineDataStore` (same ID 38022).

## AUTO-LTC-030 — `LL - Limpieza Tabla Recomendados Interna` (6477190) — inactive, incomplete

Created 2026-10-01; scheduled every 15 min but **inactive**. Pages `GET /api/recomendaciones-servicios` (phone not null, `mensajesEnviados` null or 1) and aggregates; no further action (warning "not using the data"). Unfinished cleanup attempt. Contains a literal Strapi token.

## AUTO-LTC-031 — `Automation Testing` (4141246) — inactive, obsolete

Searches `LL_RecommendationsMade` for a hard-coded phone fragment and deletes matching keys **in `LL_MessagesHistory`** (wrong store — keys never match). 14 orphan modules incl. WA templates with literal tokens. Candidate for deletion after client approval.

## Firbot development tooling (created 2026-11-05/06, all **inactive**)

| ID | Exact name | Make ID | What it does | Risk |
|---|---|---|---|---|
| `AUTO-LTC-032` | Firbot - Blueprint Patcher | 6919674 | Reads a scenario blueprint through the Make API (connection `Firbot - Make API escenarios` 12169302, API key) and applies up to 8 find/replace pairs, then `PATCH /v2/scenarios/{id}?confirmed=true` if `dryRun=false` and each fragment occurs exactly once; logs to `Firbot_PatcherLog` | Can **modify any production scenario** of the team; text-level patching bypasses the editor; log stores blueprint fragments |
| `AUTO-LTC-033` | Firbot - Consulta Strapi (temporal) | 6920671 | Generic `GET /api/{path}` to Strapi, stores up to 8,000 chars of the response in `Firbot_PatcherLog` | Copies production (personal) data into a Data Store |
| `AUTO-LTC-034` | Firbot - Simulador WhatsApp (temporal) | 6920717 | POSTs an arbitrary payload to the **main production webhook** (simulated `wamid.SIM…` ids) | Simulated messages hit production and Strapi logs |
| `AUTO-LTC-035` | Firbot - Borrar registros de prueba (temporal) | 6932098 | `DELETE /api/recomendaciones-servicios/{id}` restricted by filter to ID `1230` | Destructive Strapi write (narrowly scoped) |
| `AUTO-LTC-036` | Firbot - Test IA extractor (temporal) | 6933016 | Runs the ContextCatcher + Data Extractor prompts with a caller-chosen model | Prompt copy can drift from production |
| `AUTO-LTC-037` | Firbot - Buscar registros de prueba (temporal) | 6933260 | Tests the 10-contact limit message with dummy data, logs to `Firbot_PatcherLog` | None (dummy data) |

**Context (confirmed from Make execution provenance):** development of the RecMulti family on 2026-11-05 was performed **directly in production** using these tools and Make MCP `scenarios_run` calls, consistent with the stated absence of a test environment. Names marked "(temporal)" indicate intended removal; removal requires an authorised change (not done here).
