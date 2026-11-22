---
title: "Decision Registry"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# 08 — Decision Registry

The following are **observed architecture/operating choices**, recorded as initial ADR topics. Exact decision dates, approvers and considered alternatives were not supplied; these are **not retroactive claims of formal meetings**.

| Decision ID | Decision date | Topic | Status | Current adopted approach | Rationale / context | Consequences / verification |
|---|---|---|---|---|---|---|
| `ADR-LTC-001` | Unknown | WhatsApp-first service discovery | Observed current design | Nexo via WhatsApp Business Cloud API | Shareable chatbot fits existing WhatsApp recommendation behavior | Verify user flows, Meta subscription and monitoring |
| `ADR-LTC-002` | Unknown | Make account ownership | Observed current design | Client-owned Make account; main + child scenarios | Technical and operational isolation per client | Verify exact org/team, roles, shared account risk |
| `ADR-LTC-003` | Unknown | Data/platform ownership boundary | Observed current design | Client maintains Strapi and website; Firbot integrates with selected collections, reading ads only | Avoid ownership confusion | Verify endpoint scopes, service account policies |
| `ADR-LTC-004` | Unknown | No separate testing environment | Observed current constraint | Production used without separate staging | Not an endorsement; historical reasons unknown | Elevated deployment risk; propose a test strategy separately |
| `ADR-LTC-005` | Unknown | Technical notifications | Observed current design | Gmail for errors; WhatsApp for users | Keep technical alerts out of user conversation | Verify routing, recipients, retries and coverage |

## Not yet accepted as decisions

- Formal monthly maintenance retainer (business proposal, not current state).
- New separate testing environment (proposal, not current state).
- Automated documentation refresh by Claude/Make MCP (planned workflow; not a live production automation).

## Next steps

For each ADR, validate the decision owner, date, alternatives, trade-offs and whether the choice remains active. Create an individual file from [`../templates/DECISION.template.md`](../templates/DECISION.template.md) when needed.
