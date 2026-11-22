---
title: "AUTO-LTC-007/008/009/011 — Shared utility subscenarios"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make scenarios 4226818, 5421473, 5694920, 5892850; sanitized exports"
---

# Shared utility subscenarios

## AUTO-LTC-007 — `Envio de Notificaciones de Error Chatbots` (4226818)

- **Status:** active, on-demand; created 2026-02-24, last edit 2026-03-22. Called from 23 scenarios (every Nexo scenario with error handling).
- **Inputs:** `scenarioName`*, `scenarioURL`*, `emailErrorMessage`*, `toRecipients`* (comma-separated), `CCRecipients`, `BCCRecipients`, `clientPhoneNumber`, `wppErrorMessage`, `wppReplyNeeded`*.
- **Logic:** split recipient lists → **Microsoft 365 / Outlook** module `microsoft-email:createAndSendAMessage` (connection `LMelman Firbot Connection`, ID 5431897, type `azure`, owned by a Firbot individual) sends HTML e-mail "Error on {scenario}" with execution link. If `wppReplyNeeded` and phone + message present → sends the apology text to the end user via WA (literal token).
- **Conflict — verification required:** onboarding stated *Gmail* is the error channel; the live configuration sends through a **Microsoft (Outlook) connection**. Recipients passed by callers are Firbot mailboxes plus, in some callers, a client/stakeholder personal Gmail address (values redacted). Gmail may therefore be a *recipient* mailbox, not the sender.
- **Risk:** single point of failure for alerting tied to an individual's Microsoft account; if the OAuth connection expires alerts stop silently (**Inference**).

## AUTO-LTC-008 — `LL - Log Message` (5421473)

- **Status:** active, on-demand; created 2026-06-17, last edit 2026-09-14. Called by 20 scenarios (most outbound/inbound messages).
- **Inputs:** `SaveInDataStore`*, `Telefono`*, `Nombre`*, `Direccion`* (`Salida`/`Entrada`), `Mensaje`*, `Timestamp`*, `ClaveExterna`*, `VarianteId`, `RecomendacionId`, `Metadata` (JSON text), `AdminMode`, `CurrentlyProcessing`*. **Output:** `DataStoreKey`.
- **Logic:** if `SaveInDataStore` → `AddRecord` in `LL_MessagesHistory` (timestamp: now for outbound, WA unix ts converted to Buenos Aires for inbound) and keep key. Then `POST /api/wpp-bot/mensajes` (header `X-Bot-Token` literal) with the message. Response `errores≥1` or `omitidos≥1` → error e-mail. HTTP error → e-mail + Ignore. Returns `DataStoreKey`.
- **Note:** the "omitidos" branch CCs a personal Gmail address hard-coded in the module.

## AUTO-LTC-009 — `LL - Subscenario Send Sticker` (5694920)

- **Status:** active, on-demand; created 2026-07-18, last edit 2026-08-09. Caller: main scenario.
- **Inputs:** `StickerID`* ∈ {Welcome, Celebrating, Search, GivingStar, Success, BlinkAndLike, SearchingInCM}, `ClientPhone`*, `ClientName`.
- **Logic:** Google Drive `getAFile` (connection `My Google Drive connection` 9967715, client Google account; file IDs mapped per sticker in one Drive folder) → upload to WhatsApp media (`POST /{phone-id}/media`, `image/webp`) → send sticker message → log (`SaveInDataStore=true`). Each send re-uploads the media (no caching of media IDs).

## AUTO-LTC-011 — `Sleep n Seconds` (5892850)

- **Status:** active, on-demand; created 2026-08-09, last edit 2026-09-17. Caller: main scenario (async, `seconds=8`).
- **Inputs:** `seconds`* (default 8, max 300), `wa_id`*.
- **Logic:** sleep n s → search `LL_MessagesHistory` for outbound (`Salida`) messages to this user in the last n+2 s → if none, send a random "processing" message ("Un segundo, ya te ayudo con eso 😊" etc.). Purpose: perceived responsiveness while the main flow runs AI calls. The notice itself is **not logged** to Strapi/DS.
