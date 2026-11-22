---
title: "AUTO-LTC-005 — LL - Recomendar Servicio"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make scenario 2637777; sanitized export ll-recomendar-servicio__2637777__2026-11-22.sanitized.json"
---

# AUTO-LTC-005 — `LL - Recomendar Servicio` (2637777)

| | |
|---|---|
| Status | Active, on-demand, DLQ enabled; created 2025-08-04, last edit 2026-06-19 |
| Caller | Main scenario only (3 call sites, wait=true) |
| Inputs | `Username`, `CellphoneNumber`, `Timestamp`, `ProviderName`, `ProviderContact`, `ProviderService`, `ProviderZone`, `isExact` |
| Outputs | none |
| Purpose | Register a provider recommended by a resident in Strapi `LL - Recomendaciones de servicios` (single recommendation) |

## Logic

1. Escape inputs; `genericProviderContact` = phone without spaces/`+`, `54911`→`11`.
2. Send "processing" WA text (+log).
3. `GET /api/recomendaciones-servicios?filters[telefonoServicio][$containsi]=<generic phone>`.
4. **Not found:**
   - `isExact=true`: resolve category ID (`categorias-de-servicios`) and zone ID (`barrios-agenda`) → `POST` recommendation with `nombrePrestador`, `telefonoServicio`, `barrioCliente`, `categoriaServicio.connect`, `barrioServicio.connect`, `Recomendadores=[{user: phone}]`. On error → fallback `POST` without relations (only name/phone/zone/`observacion`) then `Resume`.
   - `isExact=false`: `POST` with `observacion = "Barrio ingresado: … Servicio ingresado: …"` and `Recomendadores` (no relations). On error → e-mail + `Break` retry 3×15 min.
5. **Found:** `PUT /api/recomendaciones-servicios/{id}` appending `{user: phone}` to `Recomendadores` (string concatenation of the existing JSON). On error → e-mail + retry 3×15 min. *Note:* it does not check whether this user already recommended the provider (RecMulti 4 does) — duplicates possible (**Inference**).
6. Send confirmation "¡Felicitaciones! *X* se registró…" + interactive buttons (+ logs with `RecomendacionId`), then trim `LL_MessagesHistory` keeping the last record.

Downstream: Strapi `afterCreate` on the recommendation fires webhook `Creacion-Recomendado-Strapi` → AUTO-LTC-016 sends the template to the provider (**Confirmed** payload shape; Strapi-side trigger **Inference**).
