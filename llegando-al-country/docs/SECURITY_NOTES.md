---
title: "Security Notes"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# Security Notes — Initial Finding

## Confirmed finding: embedded access credentials in submitted blueprint

A provided `LL - Chatbot Recomendacion de Servicios` JSON blueprint contains **literal Meta/WhatsApp Bearer access tokens** in the `Authorization` headers of some HTTP modules (seen in the submitted source during onboarding on **2026-11-22**).

- **This confirms sensitive content was present in the exported artifact.** It does **not** prove external compromise, ongoing credential validity or misuse.
- Original blueprint **deliberately excluded** from this ZIP and from Git.
- No access tokens, full endpoint payloads or private message content are reproduced here.
- **High-priority action:** have the authorised Meta/Make owner rotate or revoke those credentials, review current connections, access rights and historical sharing, and replace literal credentials with secure credential-managed references where supported.
- Treat *all* Make exports as potentially sensitive until both automated scanning and manual review finish. Data Store exports and screenshots may contain personal data too.

## Repo controls

- `exports/make/private/` is ignored; suitable only for **local temporary raw exports**, not a secure vault.
- `exports/make/sanitized/` is for redacted, reviewed versioned exports. Explicit human approval before committing.
- Never put personal contact names/phones, customer messages, real record contents or secret values in Markdown documentation.
- Do not assume Git history can be cleaned by deleting files after committing them. Scan **before first push**.

## Follow-up verification

- [ ] Token rotation/revocation verified by platform owner.
- [ ] Impact/reachability assessed and incident classification decided.
- [ ] All child exports scanned for tokens in headers, query strings, bodies, and module connection fields.
- [ ] Make/Meta permission scopes reviewed and restricted to minimum needed.
- [ ] Sanitized exports validated for meaningful non-secret technical completeness.
- [ ] Team confirms safe policy for sharing any exports with external AI assistants or platforms.
