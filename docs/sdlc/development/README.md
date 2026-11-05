# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### DEV-PLAN-001 · approved · source: plan:v1

Development plan version 1 is approved and organizes the notes app build into 5 sprints of capacity 20 each, spanning account/auth, note creation, organization, offline/sync, and search/trash features.

Plan status: approved, version 1. Sprint 1 goal: Account sign-up/login/logout and private-notes authorization foundation (capacity 20). Sprint 2 goal: Core note creation and rich text formatting (capacity 20). Sprint 3 goal: Auto-save, folders, note renaming and cross-device sync core (capacity 20). Sprint 4 goal: Offline PWA support, reconnect sync and trash (capacity 20). Sprint 5 goal: Notes list, folder moves, search and trash restore (capacity 20).

**Related:** US-001, US-002, US-003, US-004, US-005, US-006, US-007, US-008, US-009, US-010, US-011, US-012, US-013, US-014, US-015, US-016, US-017, US-018

- ⚠ Input does not state which specific stories/tasks are assigned to which sprint - only sprint-level goals are given; mapping below is inferred from goal wording, not stated explicitly.
- ⚠ No execution status (in-progress/done, commits, PR links, test results) reported for any sprint yet.

### EPIC-001 · approved · source: plan:EPIC-001

Epic covers account sign-up, login, logout, and keeping notes private to the owning account. Aligns with Sprint 1's goal of an auth and authorization foundation.

US-001 Sign up with email and password (8 pts, backend-agent), broken into: US-001-T1 add users table migration and password hashing (backend-agent); US-001-T2 implement POST /auth/signup endpoint with validation (backend-agent); US-001-T3 build sign-up form UI with validation feedback (frontend-agent). US-002 Log in to my account (5 pts, backend-agent) - no task breakdown given. US-003 Keep notes private to my account (3 pts, backend-agent) - no task breakdown given. US-004 Log out (2 pts, backend-agent) - no task breakdown given.

**Related:** US-001, US-002, US-003, US-004

- ⚠ No completion or test status reported for any item in this epic.
- ⚠ US-002, US-003, US-004 lack task-level breakdowns, unlike US-001.

### EPIC-002 · approved · source: plan:EPIC-002

Epic covers creating a new note, rich text editing/formatting, and auto-saving changes while editing. Core creation/formatting work aligns with Sprint 2's goal; auto-save is also named explicitly in Sprint 3's goal.

US-005 Create a new note (8 pts, backend-agent): US-005-T1 add notes table migration (backend-agent); US-005-T2 implement POST /notes and GET /notes/{id} endpoints (backend-agent); US-005-T3 build new note creation flow and editor shell (frontend-agent). US-006 Edit note content with rich text formatting (8 pts, frontend-agent): US-006-T1 integrate rich text editor with formatting toolbar (frontend-agent); US-006-T2 extend PUT /notes/{id} to persist rich content and checkbox state (backend-agent); US-006-T3 render saved formatting and checkbox state on reopen (frontend-agent). US-007 Auto-save changes while editing (5 pts, frontend-agent) - no task breakdown given.

**Related:** US-005, US-006, US-007

- ⚠ No completion or test status reported for any item in this epic.
- ⚠ US-007 has no task-level breakdown.
- ⚠ Sprint assignment for US-007 is ambiguous: grouped here under Sprint-2-flavored epic, but Sprint 3's stated goal also explicitly names 'Auto-save' - input does not confirm which sprint actually carries this story.

### EPIC-003 · approved · source: plan:EPIC-003

Epic covers browsing the notes list, creating/managing folders, moving notes between folders, and renaming notes.

US-008 Browse notes list with titles and last-edited time (3 pts, frontend-agent). US-009 Create and manage folders/notebooks (5 pts, backend-agent). US-010 Move a note between folders (3 pts, backend-agent). US-011 Rename a note (2 pts, frontend-agent). No sub-task breakdown given for any of these stories.

**Related:** US-008, US-009, US-010, US-011

- ⚠ No task-level breakdown provided for any story in this epic.
- ⚠ Sprint 3's goal mentions 'folders, note renaming' (suggesting US-009/US-011) while Sprint 5's goal mentions 'Notes list, folder moves' (suggesting US-008/US-010) - input does not explicitly confirm which sprint each story belongs to.
- ⚠ No completion or test status reported.

### EPIC-004 · approved · source: plan:EPIC-004

Epic covers full-text search across a user's notes, aligning with Sprint 5's goal of adding search.

US-012 Search across my notes (8 pts, backend-agent): US-012-T1 add full-text search index and GET /search endpoint (backend-agent); US-012-T2 build search UI with results list and empty-state message (frontend-agent).

**Related:** US-012

- ⚠ No completion or test status reported for any item in this epic.

### EPIC-005 · approved · source: plan:EPIC-005

Epic covers deleting a note to trash and restoring a previously deleted note, aligning with Sprint 4 (trash) and Sprint 5 (trash restore) goals.

US-013 Delete a note to trash (3 pts, backend-agent) - no task breakdown given. US-014 Restore a deleted note (5 pts, backend-agent) - no task breakdown given.

**Related:** US-013, US-014

- ⚠ No task-level breakdown provided for either story.
- ⚠ No completion or test status reported.

### EPIC-006 · approved · source: plan:EPIC-006

Epic covers cross-device sync, installing the app as a PWA, reading/editing notes offline, and syncing offline changes on reconnect. Spans Sprint 3 (sync core) and Sprint 4 (offline PWA support and reconnect sync) goals.

US-015 Sync notes across devices (8 pts, backend-agent): US-015-T1 implement POST /sync/notes endpoint for batched note sync (backend-agent); US-015-T2 add client-side sync trigger and last-synced tracking (frontend-agent); US-015-T3 define conflict resolution strategy for concurrently edited notes (backend-agent). US-016 Install the app as a PWA (3 pts, frontend-agent) - no task breakdown given. US-017 Read and edit notes offline (8 pts, frontend-agent): US-017-T1 configure service worker caching for notes data and app shell (frontend-agent); US-017-T2 add IndexedDB local store for offline notes and edits (frontend-agent); US-017-T3 build offline status indicator and offline-aware editing flow (frontend-agent). US-018 Sync offline changes on reconnect (8 pts, integration-agent): US-018-T1 implement background sync registration and retry on reconnect (frontend-agent); US-018-T2 extend POST /sync/notes to merge offline batches against server state (backend-agent); US-018-T3 add conflict reconciliation to preserve both versions without data loss (integration-agent).

**Related:** US-015, US-016, US-017, US-018

- ⚠ US-016 has no task-level breakdown.
- ⚠ No completion or test status reported for any item in this epic.
- ⚠ Conflict-resolution approach (US-015-T3, US-018-T3) is only described as a planned task - no actual strategy/decision content was provided to document.
<!-- sdlc:auto:end narrative -->
