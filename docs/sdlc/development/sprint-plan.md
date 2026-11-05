# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Account sign-up/login/logout and private-notes authorization foundation

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Sign up with email and password | 8 | backend-agent | — |
| ↳ US-001-T1 | Task | Add users table migration and password hashing | — | backend-agent | — |
| ↳ US-001-T2 | Task | Implement POST /auth/signup endpoint with validation | — | backend-agent | — |
| ↳ US-001-T3 | Task | Build sign-up form UI with validation feedback | — | frontend-agent | — |
| US-002 | Story | Log in to my account | 5 | backend-agent | US-001 |
| US-003 | Story | Keep notes private to my account | 3 | backend-agent | US-002 |
| US-004 | Story | Log out | 2 | backend-agent | US-002 |

## Sprint 2: Sprint 2

Core note creation and rich text formatting

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-005 | Story | Create a new note | 8 | backend-agent | US-001, US-002, US-003 |
| ↳ US-005-T1 | Task | Add notes table migration | — | backend-agent | — |
| ↳ US-005-T2 | Task | Implement POST /notes and GET /notes/{id} endpoints | — | backend-agent | — |
| ↳ US-005-T3 | Task | Build new note creation flow and editor shell | — | frontend-agent | — |
| US-006 | Story | Edit note content with rich text formatting | 8 | frontend-agent | US-005 |
| ↳ US-006-T1 | Task | Integrate rich text editor with formatting toolbar | — | frontend-agent | — |
| ↳ US-006-T2 | Task | Extend PUT /notes/{id} to persist rich content and checkbox state | — | backend-agent | — |
| ↳ US-006-T3 | Task | Render saved formatting and checkbox state on reopen | — | frontend-agent | — |
| US-016 | Story | Install the app as a PWA | 3 | frontend-agent | US-005 |

## Sprint 3: Sprint 3

Auto-save, folders, note renaming and cross-device sync core

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-007 | Story | Auto-save changes while editing | 5 | frontend-agent | US-006 |
| US-009 | Story | Create and manage folders/notebooks | 5 | backend-agent | US-003 |
| US-011 | Story | Rename a note | 2 | frontend-agent | US-005 |
| US-015 | Story | Sync notes across devices | 8 | backend-agent | US-005, US-007 |
| ↳ US-015-T1 | Task | Implement POST /sync/notes endpoint for batched note sync | — | backend-agent | — |
| ↳ US-015-T2 | Task | Add client-side sync trigger and last-synced tracking | — | frontend-agent | — |
| ↳ US-015-T3 | Task | Define conflict resolution strategy for concurrently edited notes | — | backend-agent | — |

## Sprint 4: Sprint 4

Offline PWA support, reconnect sync and trash

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-013 | Story | Delete a note to trash | 3 | backend-agent | US-005 |
| US-017 | Story | Read and edit notes offline | 8 | frontend-agent | US-016, US-007 |
| ↳ US-017-T1 | Task | Configure service worker caching for notes data and app shell | — | frontend-agent | — |
| ↳ US-017-T2 | Task | Add IndexedDB local store for offline notes and edits | — | frontend-agent | — |
| ↳ US-017-T3 | Task | Build offline status indicator and offline-aware editing flow | — | frontend-agent | — |
| US-018 | Story | Sync offline changes on reconnect | 8 | integration-agent | US-017, US-015 |
| ↳ US-018-T1 | Task | Implement background sync registration and retry on reconnect | — | frontend-agent | — |
| ↳ US-018-T2 | Task | Extend POST /sync/notes to merge offline batches against server state | — | backend-agent | — |
| ↳ US-018-T3 | Task | Add conflict reconciliation to preserve both versions without data loss | — | integration-agent | — |

## Sprint 5: Sprint 5

Notes list, folder moves, search and trash restore

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-008 | Story | Browse notes list with titles and last-edited time | 3 | frontend-agent | US-005 |
| US-010 | Story | Move a note between folders | 3 | backend-agent | US-009, US-005 |
| US-012 | Story | Search across my notes | 8 | backend-agent | US-005, US-003 |
| ↳ US-012-T1 | Task | Add full-text search index and GET /search endpoint | — | backend-agent | — |
| ↳ US-012-T2 | Task | Build search UI with results list and empty-state message | — | frontend-agent | — |
| US-014 | Story | Restore a deleted note | 5 | backend-agent | US-013 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
