# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Sign up with email and password | US-001, US-001-T1, US-001-T2, US-001-T3 | 1 | POST /auth/signup, notes_api, postgres_db, pwa_frontend, users | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-002 | EPIC-001 | Log in to my account | US-002 | 1 | POST /auth/login, notes_api, pwa_frontend, users | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-003 | EPIC-001 | Keep notes private to my account | US-003 | 1 | GET /notes, GET /notes/{id}, notes, notes_api, users | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-004 | EPIC-001 | Log out | US-004 | 1 | POST /auth/logout, notes_api, pwa_frontend, users | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-005 | EPIC-002 | Create a new note | US-005, US-005-T1, US-005-T2, US-005-T3 | 2 | GET /notes/{id}, POST /notes, notes, notes_api, postgres_db, pwa_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-006 | EPIC-002 | Edit note content with rich text formatting | US-006, US-006-T1, US-006-T2, US-006-T3 | 2 | PUT /notes/{id}, notes, notes_api, pwa_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-007 | EPIC-002 | Auto-save changes while editing | US-007 | 3 | PUT /notes/{id}, notes, notes_api, pwa_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-008 | EPIC-003 | Browse notes list with titles and last-edited time | US-008 | 5 | GET /notes, notes, pwa_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-009 | EPIC-003 | Create and manage folders/notebooks | US-009 | 3 | GET /folders, POST /folders, folders, notes_api, postgres_db, pwa_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-010 | EPIC-003 | Move a note between folders | US-010 | 5 | PUT /notes/{id}, folders, notes, notes_api | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-011 | EPIC-003 | Rename a note | US-011 | 3 | PUT /notes/{id}, notes, notes_api, pwa_frontend | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-012 | EPIC-004 | Search across my notes | US-012, US-012-T1, US-012-T2 | 5 | GET /search, notes, notes_api, postgres_db, pwa_frontend | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-013 | EPIC-005 | Delete a note to trash | US-013 | 4 | POST /notes/{id}/trash, notes, notes_api | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-014 | EPIC-005 | Restore a deleted note | US-014 | 5 | DELETE /notes/{id}, GET /trash, POST /notes/{id}/restore, notes, notes_api | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-015 | EPIC-006 | Sync notes across devices | US-015, US-015-T1, US-015-T2, US-015-T3 | 3 | POST /sync/notes, notes, notes_api, pwa_frontend | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-016 | EPIC-006 | Install the app as a PWA | US-016 | 2 | pwa_frontend | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-017 | EPIC-006 | Read and edit notes offline | US-017, US-017-T1, US-017-T2, US-017-T3 | 4 | notes, pwa_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-018 | EPIC-006 | Sync offline changes on reconnect | US-018, US-018-T1, US-018-T2, US-018-T3 | 4 | POST /sync/notes, notes, notes_api, pwa_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
<!-- sdlc:auto:end matrix -->
