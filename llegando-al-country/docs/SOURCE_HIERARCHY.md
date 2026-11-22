---
title: "Source Hierarchy"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# Source Hierarchy and Verification Labels

Use evidence in this order: (1) current live system observed through authorised read-only access; (2) newest inspected export; (3) up-to-date canonical docs; (4) stakeholder-confirmed requirements/current behavior; (5) supporting source material; (6) recent tickets; (7) historical docs; (8) labelled inference; (9) general platform knowledge.

## Label glossary

- **Confirmed from live system:** dated observation of authenticated system or stakeholder-provided UI screenshot, with distinction noted.
- **Confirmed from inspected export:** exact reviewed snapshot with inspection date and version/date when available; not proof of current deployment.
- **Confirmed from canonical documentation:** current, validated technical doc.
- **Confirmed requirement:** user/stakeholder description of intended or confirmed operation; not automatically runtime proof.
- **Historical:** earlier behavior, requires current verification.
- **Inference:** reasonable conjecture explicitly labelled.
- **Unknown / TODO: verify:** no satisfactory evidence yet.
- **Conflict — verification required:** sources disagree; record both, do not pick silently.

For every major claim, include at least source type, observation date, and scenario/resource ID or source path. Redact secret and personal data. When a newer live observation contradicts an old export, document both rather than rewriting history without explanation.
