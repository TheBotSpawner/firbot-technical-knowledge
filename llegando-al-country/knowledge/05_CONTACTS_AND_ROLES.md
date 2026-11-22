---
title: "Contacts and Roles"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# 05 — Contacts and Roles

**Privacy rule:** use **role placeholders**, not personal names, contact emails or phone numbers, in this repository. The onboarding conversation identified human contacts, but exact personal mapping and directory are maintained separately in a client-approved contact system.

| Role | Placeholder | Responsibility | Status | Verification |
|---|---|---|---|---|
| Primary client contact / business coordination | `<Primary Client Contact>` | Main coordination with Firbot | Current | Stakeholder confirmed a primary contact; private directory required |
| Client business stakeholders | `<Client Stakeholder 2–4>` | Business review and operational feedback | Current | Names supplied in onboarding; functions TODO |
| Client technical owner / Strapi administrator | `<Country Magazine Technical Team>` | Strapi system, website, custom dashboard, data model | Current | Confirmed by stakeholder |
| Make automation developer / maintainer | `<Firbot Automation Team>` | Nexo Make scenarios and integration support | Current | Confirmed by stakeholder |
| Production incident contact | `<Support Contact — Nexo>` | Receive/triage incidents | Transitional | No formal support agreement yet; TODO |
| WhatsApp / Meta platform owner | `<Meta App / WABA Owner>` | WhatsApp numbers, Meta app, tokens, webhook configuration | Unknown | TODO |
| OpenAI billing / project owner | `<OpenAI API Owner>` | API subscription, security and capacity | Unknown | TODO |
| Gmail notification mailbox owner | `<Error Notification Mailbox Owner>` | Receive error alerts | Unknown | TODO |

## Approval / communication

- Client technical team manages Strapi, website and dashboard; Firbot is **not** the general platform administrator.
- Firbot currently provides practical issue support and enhancements, but **a formal paid maintenance contract has not been established**.
- **TODO: verify** who approves changes to production Make scenarios, allowed test window, approvals for Strapi writes, response-time expectations and emergency escalation.
- Operational user channel: WhatsApp. Technical error alerts: Gmail.
- Do not store passwords, tokens, or personal directory entries here.
