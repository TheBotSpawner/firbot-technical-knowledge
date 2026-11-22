# Llegando al Country — Technical Knowledge

This repository is the **read-only, evidence-based technical baseline** for **Llegando al Country** (Country Magazine), including its production WhatsApp assistant **Nexo**.

- **`technical-knowledge`** = verified current technical state, with provenance and open questions.
- **`automations-development`** = proposed changes, fixes and feature development (separate repository; not created here).

**Scope:** Make.com scenarios, Data Stores and webhooks; WhatsApp Business Cloud API; OpenAI; Strapi integration; error notifications; dependencies on the client website/dashboard.

**Start here:** [`knowledge/00_PROJECT_GUIDE.md`](knowledge/00_PROJECT_GUIDE.md) → [`knowledge/01_SYSTEM_MAP.md`](knowledge/01_SYSTEM_MAP.md) → [`knowledge/03_AUTOMATION_REGISTRY.md`](knowledge/03_AUTOMATION_REGISTRY.md) → [`knowledge/automations/make/README.md`](knowledge/automations/make/README.md).

## Status on 2026-11-22

- Nexo is in production with real users (stakeholder).
- **Live Make inventory completed (read-only):** org `Llegando al Country` (4655020), team 1163364 — **37 scenarios (29 active / 8 inactive), 9 Data Stores, 17 webhooks, 5 connections**, all documented; 37 sanitized blueprint exports with manifest.
- Strapi used by Make through 9 endpoints/collections; `LL - Anuncios` confirmed **read-only** from Make. Full Strapi models not inspected (no access).
- No separate test environment; development was observed running in production.

## Security first

The live scenarios contain **literal credentials** (1 WhatsApp token in 19 scenarios, 2 Strapi API tokens in 16, 1 Strapi bot token in 3) — rotation and migration required by the authorised owners. See [`docs/SECURITY_NOTES.md`](docs/SECURITY_NOTES.md).

Raw exports live only in `exports/make/private/` (Git-ignored). Only sanitized, scanned exports are versioned in `exports/make/sanitized/`.

## Repository layout

```text
knowledge/
  00..09 canonical registries
  automations/make/     9 detail docs covering all 37 scenarios + dependency map
  schemas/make/         9 Data Store schemas + usage matrix
  schemas/strapi/       Strapi collections/endpoints used by Make
exports/make/           sanitized/ (37 JSON), manifest.md, private/ (ignored)
docs/                   security notes, gaps, checklist, Make handoff, source hierarchy
templates/              document templates
CLAUDE.md               rules for AI assistants
```

## Key findings (details in `knowledge/07_INCIDENT_REGISTRY.md`)

1. Literal tokens in production scenarios (critical).
2. Main WhatsApp webhook has no authentication.
3. Contact-time window for templates bypassed by test conditions; off-time queue unused.
4. Error e-mails are sent via a personal Microsoft 365 connection (conflicts with "Gmail" statement).
5. Functional defects: Revista call input typo; Pedido Review logs hard-coded test identity; impossible alert condition in Nueva Opinion.
6. Firbot development tooling (incl. a blueprint patcher) and unused webhooks remain in the production team.

## Authoring protocol

Read `CLAUDE.md` and `docs/SOURCE_HIERARCHY.md`; use read-only access; preserve canonical IDs; record gaps and conflicts instead of guessing; never change live resources from this repository.
