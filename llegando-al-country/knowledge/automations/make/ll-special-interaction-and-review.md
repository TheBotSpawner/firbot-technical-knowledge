---
title: "AUTO-LTC-010/022 — Special Interaction and Pedido Review"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make scenarios 5695064, 5625466; sanitized exports"
---

# Special Interaction and review-request flow

```mermaid
sequenceDiagram
  participant Web as Website (Contactar button)
  participant PR as LL - Pedido Review 5625466
  participant RR as DS LL_ReviewRequests
  participant WA as WhatsApp user
  participant Main as Main 2505419
  participant SI as Special Interaction 5695064
  Web->>PR: webhook Boton-Contactar (telefono, servicio, usuario)
  PR->>PR: GET /api/servicios/{id}?populate=usuario + OpenAI category
  PR->>WA: template llegando_click_boton_contactar (quick replies review_yes|id / review_no|id)
  PR->>RR: AddRecord status=pending
  WA->>Main: button "Sí, ya lo hice" / "No, no lo contacté"
  Main->>SI: WhichSpecialEvent=Contactar (payload, button text)
  SI->>RR: search by reviewRequestId → update status/response
  SI->>WA: review link or thanks
```

## AUTO-LTC-010 — `LL - Subscenario Special Interaction` (5695064)

- **Status:** active, on-demand; created 2026-07-18, last edit 2026-11-06. Caller: main scenario (2 call sites).
- **Inputs:** `WhichSpecialEvent`* ∈ {Contactar, CompartirAnuncio, Reset, Revista, DejarOpinion, EditarMiAnuncio, AnunciarServicio, CuantoCuesta, QueEsLlegando}, `wa_id`, `ContactName`, `NotGeneral` {ButtonPayload, ButtonText, ContactToText, DataStoreKey, DataStoreMessage, IncomingMessageID, MessageType, TimeStamp}.
- **Routes:** `CompartirAnuncio` (find ad by slug = button payload in `GET /api/servicios`, send copy-paste share text), `Revista` (subscription link), `DejarOpinion` (review link), `EditarMiAnuncio` (instructions), `Contactar` (review answer, updates `LL_ReviewRequests`), `AnunciarServicio`, `QueEsLlegando`, `CuantoCuesta` (static texts). Each route logs and resets the processing flag in `LL_MessagesHistory` (key `NotGeneral.DataStoreKey`).
- **Finding:** enum value `Reset` has **no route** (dead option). The main scenario's Revista call (#567) passes `WichSpecialEvent` (typo) — see FIND-LTC-009.
- Strapi: `GET /api/servicios` only (read-only).

## AUTO-LTC-022 — `LL - Pedido Review` (5625466)

- **Status:** active; webhook `Boton-Contactar` (hook 2560154), immediate, DLQ enabled; created 2026-07-10, last edit 2026-07-28.
- **Trigger payload:** `tipo`, `telefono`, `usuario{id,nombre}`, `servicio{id,nombre,slug,url}`, `contacto{tipo,fecha}`, `debug`.
- **Logic:** clean phone → `GET /api/servicios/{id}?populate=usuario` → OpenAI `Detect Category` (`gpt-4o-mini`, output `category`, prompt completes "¿Llegaste a contratarlo para [categoría]?") → `reviewRequestID = review_<serviceId>_<phone>_<unix ts>` → WA template **`llegando_click_boton_contactar`** with quick-reply payloads → `AddRecord` in `LL_ReviewRequests` (status `pending`) → log.
- **Errors:** Strapi/OpenAI → e-mail + `Break` retry 3×15 min; WA send → e-mail + Ignore.
- **Finding (FIND-LTC-010):** the log call (#18) uses **hard-coded test values** for `Nombre`, `Telefono` and the `slug`/`url` inside `Metadata` instead of the real recipient — every logged outbound message of this flow is attributed to the same fixed person in Strapi (`LL - WhatsApp Mensaje`).
- No timing window and no deduplication: every click sends a template.
