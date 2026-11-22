---
title: "AUTO-LTC-016..021, 023..025 — Strapi-triggered outbound WhatsApp notifications"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make scenarios 4222809, 4227025, 4378165, 4469351, 4469369, 5146890, 5822771, 5822780, 5822785; sanitized exports"
---

# Strapi-triggered outbound notifications (provider/advertiser lifecycle)

These scenarios are **independent** of the chat: they start from Make custom webhooks called by the client platform (Strapi lifecycle hooks / website backend — **Inference**, emitter not visible from Make) or from a schedule, and send **WhatsApp template messages** (business-initiated, outside the 24 h window). All use the WhatsApp phone-number ID `717278908136135` with a **literal Bearer token** and log through `LL - Log Message`.

## Contact-window gating and the off-time queue

Designed rule: send only Mon–Fri 18:00–22:00 or Sat–Sun 10:00–22:00 (America/Argentina/Buenos_Aires); otherwise store `{Payload, WebhookToSend}` in `LL_OffTimeRecomendations` and let `LL - Send Template On Time` re-post it later.

**Live configuration (FIND-LTC-003):** in all four producers the "Check If is a Good Time" filter has an extra OR group that is always true (`test = test` in 4222809 / 4469351 / 4469369, `Testing = Testing` in 4378165). **Effect (Inference, consistent with 0 queued records):** templates are sent at any hour and the off-time queue is never used.

| Canonical ID | Exact name | Make ID | Trigger (hook ID) | Templates | Strapi | Data stores | Status |
|---|---|---|---|---|---|---|---|
| `AUTO-LTC-016` | LL - Envio de Mensaje Recomendado | 4222809 | `Creacion-Recomendado-Strapi` (1925734), `maxResults=1000`, sequential | `llegando_contacto_recomendados_a` / `_b` / `_c` | POST `/wpp-bot/codigo`; GET `categorias-de-servicios`; PUT `recomendaciones-servicios.mensajesEnviados=1` | `LL_RecommendationsMade` (R,C), `LL_OffTimeRecomendations` (C) | Active |
| `AUTO-LTC-017` | LL - Envio de Mensaje Recomendados Previos | 4227025 | none (on-demand, never called) | — | — | `LL_RecommendationsMade` (R) | Active but **inert** (2 modules + 7 orphans) |
| `AUTO-LTC-018` | LL - Anuncio Publicado | 4378165 | `Codigo-Verificacion-WPP-Strapi` (1999490) | `llegando_new_post_for_creators`, `llegando_new_post_for_recommenders` | GET `servicios/{id}`, GET `recomendaciones-servicios` by coupon | `LL_OffTimeRecomendations` (C) | Active |
| `AUTO-LTC-019` | LL - Nueva Opinion Anuncio | 4469351 | `NewPostOpinionStrapi` (2039466) | `llegando_first_post_review`, `llegando_post_5_reviews` | GET `opiniones` (count), GET `servicios/{id}` | `LL_OffTimeRecomendations` (C) | Active |
| `AUTO-LTC-020` | LL - Nueva Visita Anuncio | 4469369 | `NewPostVisitStrapi` (2039478) | `llegando_post_20_visits` | GET `servicios/{id}` | `LL_OffTimeRecomendations` (C) | Active |
| `AUTO-LTC-021` | LL - Send Template On Time | 5146890 | Schedule: every 15 min restricted to 10:00–10:01 and 18:00–18:01 daily (≈2 runs/day) | — (replays payloads) | — | `LL_OffTimeRecomendations` (S,R,D) | Active |
| `AUTO-LTC-023` | LL - Onboarding Paso 2 | 5822771 | `Onboarding-Paso-02` (2642230) | `llegando_share_your_profile` | — | — | Active |
| `AUTO-LTC-024` | LL - Onboarding Paso 3 | 5822780 | `Onboarding-Paso-03` (2642233) | `llegando_no_views` | GET `servicios/{id}` (`hit_20_visitas_enviado`) | — | Active; **1 item in DLQ** |
| `AUTO-LTC-025` | LL - Onboarding Paso 4 | 5822785 | `Onboarding-Paso-04` (2642237) | `llegando_ask_for_reviews` | — | — | Active |

There is **no "Onboarding Paso 1" scenario**: webhook `Onboarding-Paso-01` (2642224) exists but is not attached to any scenario (FIND-LTC-012). Onboarding Paso 3's webhook module still carries the stale label `Onboarding-Paso-01` while bound to hook 2642233 (`Onboarding-Paso-03`).

## AUTO-LTC-016 — provider outreach after a recommendation

1. Filter: `modelo = ll-pre-servicio` and `evento = afterCreate`.
2. (Time window — bypassed.) `POST /api/wpp-bot/codigo` → coupon `codigo` (`X-Bot-Token` literal).
3. Normalise phone, search `LL_RecommendationsMade` (`contains` on normalised phone). **If already contacted → stop** (idempotency).
4. OpenAI `Name Extractor` (`gpt-6-luna`), read category name.
5. **A/B test:** if a category/service name is available, template `…_a` or `…_b` is chosen from team variable `ABTesting` and the variable is flipped after each send via `make:updateAVariable` (connection `My Make (API key) connection` 9953737); without category → template `…_c`.
6. Log (with `VarianteId`/`RecomendacionId`), `PUT mensajesEnviados=1`, `AddRecord` in `LL_RecommendationsMade`.

## AUTO-LTC-018 — ad published

GET the ad with `whatsapp`, `nombre`, populated relations → send `llegando_new_post_for_creators` to the advertiser (ad `whatsapp` or owner `usuario.numero`) with the ad link → find recommendations that share the ad's coupon (`cuponUsado.cupon`), regex-extract `{name: phone}` pairs from `Recomendadores` and send `llegando_new_post_for_recommenders` to each recommender. Missing data → error e-mail.

## AUTO-LTC-019 — new review

Count published+draft reviews for the ad; total = 1 → `llegando_first_post_review`, total = 5 → `llegando_post_5_reviews`. The "Empty Data" error route requires `total = 1 AND total = 5` (impossible) → never fires (FIND-LTC-011).

## AUTO-LTC-020 — 20 visits

GET ad → send `llegando_post_20_visits` with name and link. The Strapi flag `hit_20_visitas_enviado` is not written by Make (presumably set by the emitter — **Inference**).

## AUTO-LTC-023/024/025 — advertiser onboarding follow-ups

Each receives `servicio{whatsapp,…}`; if `whatsapp` is empty → error e-mail; else send its template with quick-reply payload = ad slug (answers are handled by the main scenario as special events, e.g. `CompartirAnuncio`). Paso 3 sends only if `hit_20_visitas_enviado = false`. Error handling: e-mail + `Break` retry 3×1 min (DLQ enabled).

## AUTO-LTC-021 — off-time replay

Runs at 10:00 and 18:00; proceeds if ≥1 record and (weekend or weekday 11:00–22:00) → for each record POST `Payload` to `WebhookToSend` → delete the record. On HTTP failure → error e-mail + `Ignore`; because the delete module comes after the HTTP module, the failed record is not deleted and is retried on the next run (**Inference** from module order).
