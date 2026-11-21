---
status: Draft
last_modified: 2026-11-21
client_slug: weincenter-loerrach
---

# Naming and ID Conventions

## Candidate conventions — pending approval

| Entity | Stable prefix | Example |
|---|---|---|
| System | `SYS-<DOMAIN>-NNN` | `SYS-ORD-001` |
| Automation | `AUTO-<DOMAIN>-NNN` | `AUTO-ORD-001` |
| Data | `DATA-<DOMAIN>-NNN` | `DATA-ORD-001` |
| Component | `COMP-<DOMAIN>-NNN` | `COMP-ORD-001` |
| Incident | `INC-NNN` | `INC-001` |
| Decision | `ADR-NNN` | `ADR-001` |
| Document | `DOC-NNN` | `DOC-001` |

## Rules

- Client slug: `weincenter-loerrach` (proposed).
- Markdown filenames: lowercase-kebab-case, except template registry names (`00_PROJECT_GUIDE.md`, etc.) which remain exactly as specified.
- Do not change existing production resource names for aesthetic consistency.
- Record the **exact** existing cloud flow name, desktop flow name, SharePoint list/file name and native vendor IDs separately from internal canonical IDs.
- Never recycle IDs after retirement.
- Keep any source-language or platform-specific spelling as actually configured.
- Treat the Hawesko tracking list spelling and exact cloud-flow names as TODO: verify.
- Versions of exported solutions should contain export date, source tenant/environment and version from package where available.
