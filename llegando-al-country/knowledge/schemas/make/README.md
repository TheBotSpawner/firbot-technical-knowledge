---
title: "Make Data Store schemas — index"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
---

# Make Data Store schemas

Organization `Llegando al Country` (ID `4655020`), team `My Team` (ID `1163364`), zone `us2.make.com`.
All 9 Data Stores of the team are documented. Field definitions come from the Make data structures; **no record contents were exported**.

| Schema ID | Data ID | Exact name | Make DS ID | Structure ID | Records (2026-11-22) | Role | Doc |
|---|---|---|---|---|---|---|---|
| `SCHEMA-LTC-005` | `DATA-LTC-005` | `Firbot_PatcherLog` | 193874 | 568881 | 20 | Firbot dev-tooling log (not production) | [doc](firbot-patcherlog.md) |
| `SCHEMA-LTC-006` | `DATA-LTC-006` | `LL_MessagesHistory` | 38022 | 150742 | 1 | Conversation memory + processing lock | [doc](ll-messageshistory.md) |
| `SCHEMA-LTC-007` | `DATA-LTC-007` | `LL_MultiRecBatch` | 193870 | 568877 | 0 | Multi-recommendation tray | [doc](ll-multirecbatch.md) |
| `SCHEMA-LTC-008` | `DATA-LTC-008` | `LL_OffTimeRecomendations` | 101658 | 377659 | 0 | Off-hours notification queue | [doc](ll-offtimerecomendations.md) |
| `SCHEMA-LTC-009` | `DATA-LTC-009` | `LL_PermissionsList` | 76312 | 280435 | 5 | Admin-mode allow-list | [doc](ll-permissionslist.md) |
| `SCHEMA-LTC-010` | `DATA-LTC-010` | `LL_RecommendationsMade` | 80766 | 295935 | 285 | Providers already contacted (dedup) | [doc](ll-recommendationsmade.md) |
| `SCHEMA-LTC-011` | `DATA-LTC-011` | `LL_ReviewRequests` | 123790 | 441583 | 12 | Review-request state | [doc](ll-reviewrequests.md) |
| `SCHEMA-LTC-012` | `DATA-LTC-012` | `LL_Users` | 193869 | 568876 | 2 | Per-user remembered neighbourhood | [doc](ll-users.md) |
| `SCHEMA-LTC-013` | `DATA-LTC-013` | `LL_WelcomeContactsMade` | 76313 | 280440 | 9 | Welcome-campaign queue/register | [doc](ll-welcomecontactsmade.md) |

## Data store ↔ scenario matrix

R = search/read, C = add, U = update/overwrite, D = delete, S = stats.

| Scenario (Make ID) | MessagesHistory | MultiRecBatch | OffTime | Permissions | RecMade | ReviewReq | Users | Welcome | PatcherLog |
|---|---|---|---|---|---|---|---|---|---|
| Chatbot main (2505419) | R C U D | R | | R | | | U | | |
| Delete Messages (2629639) | R D | | | | | | | | |
| Buscar Servicio por Zona (2637743) | R U D | | | | | | | | |
| Recomendar Servicio (2637777) | R D | | | | | | | | |
| Admin Mode (4133823) | R C D | | | | | | | | |
| Enviar Bienvenida (4137315) | | | (orphan only) | | | | | R U | |
| Agregar Contactos de Bienvenida (4199053) | | | | | | | | R C | |
| Envio de Mensaje Recomendado (4222809) | | | C | | R C | | | | |
| Envio de Mensaje Recomendados Previos (4227025) | | | | | R | | | | |
| Anuncio Publicado / Nueva Opinion / Nueva Visita | | | C | | | | | | |
| Send Template On Time (5146890) | | | S R D | | | | | | |
| Log Message (5421473) | C | | | | | | | | |
| Pedido Review (5625466) | | | | | | C | | | |
| Special Interaction (5695064) | U D | | | | | R U | | | |
| Sleep n Seconds (5892850) | R | | | | | | | | |
| RecMulti 1 (6920256) | | R | | | | | R | | |
| RecMulti 2 (6920153) | | C/U | | | | | | | |
| RecMulti 3 (6920171) | | U D | | | | | | | |
| RecMulti 5 (6920183) | R D | U D | | | | | U | | |
| Automation Testing (4141246, inactive) | D | | | | R | | | | |
| Firbot tooling (6919674, 6920671, 6932098, 6933260 — inactive) | | | | | | | | | C |

## Unused data structures (not bound to any data store)

`BarriosData` (155821), `BarrioServicio` (158475), `CategoriasCM` (156605, no usage), `CategoriasDeServicio` (158472), `CategoriasServicios` (158463), `Insert Provider Result` (184381), `OffTimeRecomendation` (377666, no usage), `RecomendacionServicios` (155702), `RecomendadoresJSON` (391471, no usage), `StrapiCreateRecordEvent` (288883, used by webhooks 1925734/1925920), `wppContactsArray` (286592). They are JSON-parse/webhook structures used inside scenarios, not stores.
