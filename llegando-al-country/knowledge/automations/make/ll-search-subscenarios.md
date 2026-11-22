---
title: "AUTO-LTC-002/003/004 — Search subscenarios (Buscar Zona, Buscar Categoría, Buscar Servicio por Zona)"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API scenarios_get, read-only) on 2026-11-22"
sources: "Make scenarios 2637689, 2637692, 2637743; sanitized exports in exports/make/sanitized/"
---

# Search subscenarios

All three are **active**, scheduling `on-demand`, started by `scenario-service:StartSubscenario`, called only by the main scenario (2505419); `LL - Buscar Zona` is also called by RecMulti 1 (6920256). Created 2025-08-04. Strapi access uses a **literal Bearer token** (FIND-LTC-001).

## AUTO-LTC-002 — `LL - Buscar Zona` (2637689)

| | |
|---|---|
| Inputs | `InputZone` |
| Outputs | `zone`, `zoneFound` (`exact` / `simil` / `notFound` / `NoZone`), `zoneList` |
| Last edit | 2026-11-06 |

Logic: normalise input (lower-case, strip accents) → if length ≤ 2 return `NoZone` → `GET /api/barrios-agenda?filters[nombre][$containsi]=…` → match ⇒ `exact`. Otherwise read all neighbourhoods (paged by 40) → OpenAI `Try get similar Barrios` (`gpt-6-luna`; outputs `zone`, `zoneFound`) → second OpenAI `Validación Final` (`similar` true/false) checks that the proposed name exists in the list → `simil` or `notFound`. Errors: e-mail via AUTO-LTC-007 then `Return NotFound`.

## AUTO-LTC-003 — `LL - Buscar Categoría` (2637692)

| | |
|---|---|
| Inputs | `InputService`, `CellPhoneNumber`, `EsBuscar` (bool) |
| Outputs | `service`, `serviceFound` (`exact` / `simil` / `notFound` / `none` / `AnunciosSimilares`), `categoriesList` |
| Last edit | 2026-11-06 |

Logic: input ≤ 2 chars → `notFound`. `GET /api/categorias-de-servicios?filters[nombre][$containsi]` → exact. Else `GET /api/grupos-categorias?…` → exact. Else read all categories (pageSize 400) → OpenAI `Try get similar Categoria` → `Verify if previous GPT do it right` → `simil`/`notFound`. If not found **and `EsBuscar`**: sends WA "Un momento por favor…" (+log), pages through all active ads (`GET /api/servicios?filters[estado][$eq]=activo`, 20/page, fields `nombre`, `descripcionCorta`, `slug`), OpenAI `Search Similar Name` per page, keeps up to 3 matches → returns `AnunciosSimilares` with a list of ad URLs. Recommend path (`EsBuscar=false`) returns `notFound`.

Note: the full-catalogue AI scan is O(pages) OpenAI calls per search — cost/latency risk as the catalogue grows (**Inference**).

## AUTO-LTC-004 — `LL - Buscar Servicio por Zona` (2637743)

| | |
|---|---|
| Inputs | `searchInStrapi`, `Cellphone_Number`, `Name`, `Timestamp`, `Categoria`, `Zona` (`none` = no zone) |
| Outputs | none (sends messages itself) |
| Last edit | 2026-08-06 |

Logic: sends a "wait" WA message (+log) → builds keyword list → `GET /api/servicios?populate[barrios]=*&populate[categorias]=*&filters[estado][$eq]=activo&filters[barrios][nombre][$containsi]=<zone>&filters[$or]…[categorias][nombre]…` (paged). If ads found → WA "👍 ¡He encontrado N servicio/s…" with a link to `countrymagazine.com.ar/llegando/buscar?search=…&barrio=…`, then interactive buttons + magazine hint. If none → retry with `categoriaPrincipal`, then with `categorias` without status filter → "Lamentablemente no encontramos…" with category/zone links. Each branch then trims `LL_MessagesHistory` for the user, keeping only the last user message (prevents old intent from re-triggering).

Data written: `LL_MessagesHistory` (overwrite/delete). Strapi: **read-only** on `servicios`.
