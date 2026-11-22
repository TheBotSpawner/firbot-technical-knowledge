---
title: "Project Guide"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# 00 — Project Guide

## Purpose

This is the entry point for understanding the technical environment of **Llegando al Country**, linked to **Country Magazine**. The platform connects residents of countries/private residential neighbourhoods in Buenos Aires with locally recommended household service providers. **Nexo** is the operational WhatsApp chatbot for searching for, recommending and initiating the announcement of services.

**Source:** Stakeholder onboarding conversation (2026-11-22); public sites are context references and have not been used to verify live internals.

## Links

- Business site: https://countrymagazine.com.ar/llegando
- Magazine: https://countrymagazine.com.ar/
- Client-managed Strapi administration: https://admin.countrymagazine.com.ar/admin (authenticated; do not put credentials here)

## Authorised readers / editors

**TODO: verify** approved human developer roles, client stakeholders and AI agents; repository visibility and who is allowed to edit it. Claude Code and Firbot maintainers are *proposed authorised users*, pending repository access controls.

## Scope

- **Client-owned Make.com account:** Nexo's main scenario, subscenarios and Make Data Stores.
- **WhatsApp Business Cloud API:** messaging transport and bot channel, **without Coexistence** (stakeholder-confirmed).
- **OpenAI API:** called directly from Make for AI-backed conversation handling.
- **Client-owned Strapi:** recommended-service records, WhatsApp conversations/messages, published ads and related collections.
- **Gmail:** alerts about automation errors, not the user-facing channel.
- **Client web application/dashboard:** only the dependencies and interfaces relevant to Nexo; owner and implementation are client-managed.

## Exclusions / boundaries

- Website/backend/dashboard feature development and Strapi platform administration are **client responsibilities**; Firbot's scope is integration reads/required writes through Nexo, with **read-only access to the Anuncios collection**.
- No Microsoft ecosystem integrations were reported.
- A separate `automations-development` repository is **not included** in this ZIP.
- No intended monetisation or future maintenance agreement is documented as an already-deployed technical control.

## Current operational status

| Topic | Current state | Evidence |
|---|---|---|
| Nexo | Live in production with real users | Confirmed requirement / stakeholder account (2026-11-22) |
| Make ownership | Client-owned Make account, multiple interconnected scenarios | Confirmed by stakeholder; screenshot of Make Data Stores |
| Production vs test | No separate testing environment | Confirmed by stakeholder |
| Maintenance | Firbot assists with incidents and iterative improvements, **without a formal paid maintenance agreement** | Confirmed by stakeholder |
| Platform/data ownership | Client manages Strapi, website and statistics/message dashboard | Confirmed by stakeholder |
| Error channel | Gmail for error notifications; regular user messaging via WhatsApp | Confirmed by stakeholder and main blueprint |
| Commercial intro | A time-limited free introductory advertising period followed by monthly charges was described as tentative | **Unknown — verify** exact commercial model and implementation |

## Data sensitivity

The integrated systems process phone numbers, WhatsApp conversations, recommender and provider contact information, and possibly customer email/business details. **Sensitivity: Confidential (provisional)**. Exact classification, retention, access controls and consent requirements: **TODO: verify**.

## Default operating mode

`Read → Search → Analyse → Explain → Recommend`. The repository documents the verified deployed system. It does **not** modify live Make, Strapi, Meta, OpenAI or Gmail accounts.

## Investigating a question

1. Read `01_SYSTEM_MAP.md` and the corresponding registry (`02`, `03` or `04`).
2. Follow its linked detail file, if available.
3. Compare with date-stamped exports in `../exports/make/` and source inventory in `../source-material/`.
4. Identify evidence level, gaps and conflicts before making claims.
5. Add proposed features/fixes to a separate `automations-development` project; update this repository only after verifying a production change.

## Known gaps

See [`../docs/GAP_SUMMARY.md`](../docs/GAP_SUMMARY.md) and [`../docs/VERIFICATION_CHECKLIST.md`](../docs/VERIFICATION_CHECKLIST.md).
