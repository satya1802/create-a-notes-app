# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECH-STACK · approved · source: requirements:technology stack

Product owner approved an exact technology stack: FastAPI backend, AWS cloud, PostgreSQL 16 database, React 19 frontend.

Decided stack, to be designed against exactly (no substitutions): Backend FastAPI 0.115 (lightweight Python framework for sign-up, private-notes storage, and offline sync-batch ingestion, keeping a free app cheap and extensible). Cloud: AWS (reliable always-on hosting with backups, covering DB/API/email in one account, cheap at modest scale). Database: PostgreSQL 16 (relational storage for accounts, notes, folders, trash, last-edited timestamps; built-in full-text search serves the search box without a separate search engine). Frontend: React 19 (state-heavy writing experience: rich-text editor, auto-save, live-updating notes list; mature libraries for rich-text editing and PWA offline/background sync).

- ⚠ No architecture documentation yet translates this approved stack into actual system/component design.

### REQ-SERVICES · approved · source: requirements:services

SendGrid approved as the SaaS email provider for account verification and password-reset emails.

Service: SendGrid (saas), configured via env var SENDGRID_API_KEY. Rationale given: since sign-in uses email+password, reliable delivery of verification/reset emails is required so a locked-out user can still reach their notes; SendGrid improves inbox deliverability over spam folders. Required API key: SENDGRID_API_KEY.

**Related:** US-001, US-002

- ⚠ No deployment or architecture record yet confirms SENDGRID_API_KEY has been provisioned or integrated.

### REQ-SCOPE · approved · source: requirements:scope

Defines in-scope capabilities and explicit out-of-scope items for v1.

In scope: create/edit/auto-save notes; rich text formatting (headings, bold/italic, lists, checkboxes); private per-user accounts; organise notes into folders/notebooks; notes list with titles and last-edited time; move/rename notes between folders; full-text search; delete notes; email/password sign-up and login. Out of scope -- explicitly not to be designed or built: sharing notes with other people and real-time collaboration; embedding images or attaching files to notes. Delivery scope labeled 'lightweight'; requirements version 1.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005, EPIC-006

### US-001 · draft · source: requirements:US-001

A new visitor can sign up with an email and password to get a private, empty workspace.

Epic: EPIC-001 Account & Authentication. Priority: critical. AC-001: valid email + password meeting minimum requirements creates the account and signs the user into an empty workspace. AC-002: signing up with an email that already has an account is refused (told already registered) rather than duplicated. AC-003: invalid email or password not meeting minimum requirements shows a validation message and no account is created. Epic-level assumption: email/password only (no social/SSO login); app is free with no payments/subscriptions/billing; no specific jurisdiction named, so general web/privacy good practice applies rather than region-specific regulation.

**Related:** AC-001, AC-002, AC-003, NFR-004, EPIC-001

### US-002 · draft · source: requirements:US-002

A returning user logs in with email and password to reach their private notes.

Epic: EPIC-001. Priority: critical. AC-004: correct email+password logs the user in and shows only their own notes. AC-005: incorrect email or password shows a single authentication error without revealing which field was wrong, and the user stays logged out.

**Related:** AC-004, AC-005, NFR-003, EPIC-001

### US-003 · draft · source: requirements:US-003

A logged-in user's notes are accessible only to them; no other user can read or change them.

Epic: EPIC-001. Priority: critical. AC-006: notes list and opened notes only ever show the logged-in user's own notes. AC-007: a user who is not logged in is prevented from viewing note content directly and is prompted to log in.

**Related:** AC-006, AC-007, NFR-001, NFR-002, EPIC-001

### US-004 · draft · source: requirements:US-004

A logged-in user can log out to protect notes on a shared or public device.

Epic: EPIC-001. Priority: high. AC-008: choosing to log out ends the session; the user must log in again to view notes.

**Related:** AC-008, NFR-005, EPIC-001

### US-005 · draft · source: requirements:US-005

A logged-in user can create a new, empty note ready for editing.

Epic: EPIC-002 Note Creation, Editing & Auto-save. Priority: critical. AC-009: creating a new note opens an empty note ready for editing and it appears in the notes list. AC-010: if no title is typed, the note gets a sensible default/derived title so it can be identified in the list. Epic-level assumption: embedding images and attaching files to notes are explicitly out of scope for this version.

**Related:** AC-009, AC-010, EPIC-002

### US-006 · draft · source: requirements:US-006

A logged-in user can format note text with headings, bold/italic, lists, and checkboxes.

Epic: EPIC-002. Priority: critical. AC-011: applying heading/bold/italic/list/checkbox formatting to selected text is applied and preserved when the note is reopened. AC-012: ticking/unticking a checkbox item is saved and shown correctly on reopen. AC-013: attempting to embed an image or attach a file is not supported in this version (out of scope by design).

**Related:** AC-011, AC-012, AC-013, EPIC-002

### US-007 · draft · source: requirements:US-007

Edits are saved automatically with no manual save action, and save status is visible.

Epic: EPIC-002. Priority: critical. AC-014: pausing/stopping typing auto-saves changes without user action; the note's last-edited time updates. AC-015: closing and reopening a note shows the latest auto-saved changes. AC-016: the app indicates save status (in progress / just completed) so the user knows their work is stored.

**Related:** AC-014, AC-015, AC-016, NFR-008, EPIC-002

### US-008 · draft · source: requirements:US-008

The notes list shows each note's title and last-edited time, updated as notes change.

Epic: EPIC-003 Organising Notes into Folders. Priority: high. AC-017: each note in the list shows its title and last-edited time. AC-018: when a note's content changes and auto-saves, its last-edited time updates to reflect the most recent edit.

**Related:** AC-017, AC-018, EPIC-003

### US-009 · draft · source: requirements:US-009

A logged-in user can create named folders/notebooks to group related notes.

Epic: EPIC-003. Priority: high. AC-019: creating a folder with a name adds it to the user's list of folders. AC-020: opening a folder shows only the notes belonging to that folder.

**Related:** AC-019, AC-020, EPIC-003

### US-010 · draft · source: requirements:US-010

A user can move a note from one folder to another.

Epic: EPIC-003. Priority: medium. AC-021: moving a note to another folder makes it appear in the destination folder and no longer in the original folder.

**Related:** AC-021, EPIC-003

### US-011 · draft · source: requirements:US-011

A user can rename a note so its title reflects its content.

Epic: EPIC-003. Priority: medium. AC-022: changing a note's title saves the new title and shows it in the notes list.

**Related:** AC-022, EPIC-003

### US-012 · draft · source: requirements:US-012

A user can search across titles and content of their own notes.

Epic: EPIC-004 Full-text Search. Priority: high. AC-023: typing a word that appears in a note lists the matching notes. AC-024: a query with no matches shows a clear empty-result message. AC-025: selecting a search result opens the corresponding note. AC-026: search results only ever include notes belonging to the searching user's own account.

**Related:** AC-023, AC-024, AC-025, AC-026, NFR-001, EPIC-004

### US-013 · draft · source: requirements:US-013

A user can delete a note they no longer need, moving it to trash.

Epic: EPIC-005 Delete, Trash & Restore Notes. Priority: high. AC-027: deleting a note removes it from the active notes list and moves it to the trash. Epic-level assumption: the broader intent describes delete-with-restore via a trash; the MVP scope list literally says 'delete notes'. This is implemented as recoverable trash/restore so accidental deletion can be undone.

**Related:** AC-027, EPIC-005

### US-014 · draft · source: requirements:US-014

A user can restore a deleted note from trash, or permanently delete it.

Epic: EPIC-005. Priority: medium. AC-028: restoring a note from trash returns it to active notes with content and formatting intact. AC-029: permanently deleting a note from the trash removes it and it is no longer recoverable.

**Related:** AC-028, AC-029, EPIC-005

### US-015 · draft · source: requirements:US-015

A user's notes sync across their devices via the cloud.

Epic: EPIC-006 Cross-device Sync & Offline (PWA). Priority: critical. AC-030: a note created or edited on one device (with internet) appears on the user's other logged-in devices after syncing. Epic-level assumption: offline support is delivered as a PWA with service-worker caching and background sync on reconnect, not a native mobile/desktop app.

**Related:** AC-030, NFR-007, EPIC-006

### US-016 · draft · source: requirements:US-016

A user can install the app from a supported browser as a standalone PWA.

Epic: EPIC-006. Priority: medium. AC-031: choosing to install adds the app to the device and it can be launched as a standalone app.

**Related:** AC-031, NFR-009, EPIC-006

### US-017 · draft · source: requirements:US-017

A user can read and edit previously-loaded notes while offline.

Epic: EPIC-006. Priority: high. AC-032: after notes have been loaded, opening the app offline lets the user read cached notes and make edits. AC-033: offline edits are stored locally so they are not lost.

**Related:** AC-032, AC-033, NFR-006, EPIC-006

### US-018 · draft · source: requirements:US-018

Offline changes sync automatically to the cloud when the device reconnects.

Epic: EPIC-006. Priority: high. AC-034: regaining internet connection automatically triggers background sync of offline changes to the cloud, with no manual trigger needed. AC-035: if the same note was changed offline on one device and separately in the cloud, syncing reconciles the two versions without silently losing data.

**Related:** AC-034, AC-035, NFR-007, EPIC-006

### NFR-001 · draft · source: requirements:NFR-001

Privacy: notes must be accessible only to their owning account.

Viewing the notes list, opening a note, and running a search must all return only the logged-in user's own notes; no user can read or change another user's notes.

**Related:** US-003, US-012

### NFR-002 · draft · source: requirements:NFR-002

Security: unauthenticated users must be blocked from viewing note content.

A user who is not logged in must be prevented from viewing note content directly and must be prompted to log in first.

**Related:** US-003

### NFR-003 · draft · source: requirements:NFR-003

Security: login failures show a single non-revealing error.

A failed login attempt shows one authentication error that does not reveal whether the email or the password was wrong.

**Related:** US-002

### NFR-004 · draft · source: requirements:NFR-004

Security: sign-up enforces minimum password requirements.

A password that does not meet minimum requirements is rejected with a validation message and the account is not created.

**Related:** US-001

### NFR-005 · draft · source: requirements:NFR-005

Security: logging out fully ends the session.

Logging out must end the user's session so notes cannot be accessed again without logging back in, protecting notes on shared or public devices.

**Related:** US-004

### NFR-006 · draft · source: requirements:NFR-006

Availability: the installed app must be usable offline after notes have loaded.

Once notes are loaded, the installed app must let the user open it offline, read cached notes, and make edits with no internet connection, storing those edits locally so they are not lost.

**Related:** US-016, US-017

### NFR-007 · draft · source: requirements:NFR-007

Availability: offline changes must sync automatically without data loss.

Offline changes must sync to the cloud automatically via background sync on reconnect, without the user triggering it. Where the same note was changed both offline and in the cloud, the two versions must be reconciled without silently losing user data.

**Related:** US-015, US-018

### NFR-008 · draft · source: requirements:NFR-008

Usability: auto-save must be automatic and its status visible.

Edits must be saved automatically when the user pauses or stops typing, without any manual save action, and the app must indicate current save status so the user knows their work is stored.

**Related:** US-007

### NFR-009 · draft · source: requirements:NFR-009

Compatibility: the app must be an installable PWA, not a native app.

On a supported browser, the app must be installable, added to the device, and launched as a standalone app, delivered through service-worker caching and background sync rather than a native app.

**Related:** US-016

### NFR-010 · draft · source: requirements:NFR-010

Privacy: personal data must follow general web/privacy good practice.

Applies to the whole system: email addresses, passwords and private notes must be handled following general web and privacy good practice.

### NFR-011 · draft · source: requirements:NFR-011

Compliance (accepted risk): no region-specific regulation is addressed.

Applies to the whole system. No specific jurisdiction was named, so the product is built to general web/privacy good practice only and does not implement region-specific regulatory requirements. Recorded as an accepted risk, not a gap to fix.

### NFR-012 · draft · source: requirements:NFR-012

Scalability (accepted risk): built for modest consumer scale only.

Applies to the whole system. The product is scoped as a lightweight, free consumer app for modest individual-user scale and is not required to meet enterprise-grade or large-scale capacity targets. Recorded as an accepted risk, not a gap to fix.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-11-05

**Capabilities in scope:** Create, edit and auto-save notes, Rich text formatting (headings, bold/italic, lists, checkboxes), Private per-user account, Organise notes into folders/notebooks, Notes list showing titles with last-edited time, Move and rename notes between folders, Full-text search across notes, Delete notes, Email and password sign-up and login

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The server's job here is modest and clear: sign users up, keep each account's notes private, and accept batches of note changes when a device comes back online. FastAPI is a lightweight Python framework well suited to this straightforward sync-and-store API, and it keeps a free consumer app cheap to run and quick to extend as you add folders, trash/restore and search. |
| cloud | AWS | A notes app that syncs private data across devices needs reliable, always-on hosting with proper backups, and AWS gives you that plus room to grow without re-platforming. For a free, modest-scale consumer app it can run cheaply, and it covers the database, the API server and email in one account you manage in one place. |
| database | PostgreSQL | Everything you need to store — user accounts, notes, folders, a trash bin, and last-edited timestamps — is neatly structured and relational, which is exactly what PostgreSQL does best. It also has solid built-in full-text search, so the search box you described can be served from the database itself without adding a separate search engine, keeping this free app simple and inexpensive. |
| frontend | React | Your product lives or dies on the writing experience: a rich-text editor (headings, bold, lists, checkboxes), instant auto-save, and a notes list that updates as users type. React is built for exactly this kind of interactive, state-heavy screen, and it has the most mature libraries for the two hardest parts you described — a rich-text editor and a Progressive Web App that installs on a phone and keeps working offline with local storage and background sync. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Account & Authentication

Each user has a private account created with email and password. Notes are visible only to the account owner; there is no sharing or collaboration between accounts.

Assumption: Users sign up and log in with email and password (no social or SSO login). The app is free with no payments, subscriptions or billing. No specific jurisdiction was named, so general web/privacy good practice applies rather than region-specific regulation.

### US-001: Sign up with email and password

**Priority:** critical

> As a new visitor, I want to create an account using my email address and a password, so that I have a private space to keep my own notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am on the sign-up page and no account exists for my email | I enter a valid email and a password that meets the minimum requirements and submit | my account is created and I am signed in to my own empty workspace |
| AC-002 | I am on the sign-up page | I enter an email that already has an account | I am told the email is already registered and the account is not duplicated |
| AC-003 | I am on the sign-up page | I enter an invalid email or a password that does not meet the minimum requirements | I see a validation message and the account is not created |

### US-002: Log in to my account

**Priority:** critical

> As a returning user, I want to log in with my email and password, so that I can access my private notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-004 | I have an existing account | I enter my correct email and password and submit | I am logged in and see only my own notes |
| AC-005 | I am on the login page | I enter an incorrect email or password | I am shown an authentication error and am not logged in, without revealing which field was wrong |

### US-003: Keep notes private to my account

**Priority:** critical

> As a logged-in user, I want my notes to be accessible only to me, so that no other user can read or change my notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-006 | I am logged in | I view my notes list or open a note | I only ever see notes that belong to my own account |
| AC-007 | I am not logged in | I try to access note content directly | I am prevented from viewing it and prompted to log in |

### US-004: Log out

**Priority:** high

> As a logged-in user, I want to log out of my account, so that my notes are not accessible on a shared or public device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-008 | I am logged in | I choose to log out | my session ends and I must log in again to view my notes |

## EPIC-002: Note Creation, Editing & Auto-save

Users create and edit notes with rich text formatting and changes are saved automatically. Notes support headings, bold/italic, lists and checkboxes.

Assumption: Embedding images and attaching files to notes are out of scope for this version.

### US-005: Create a new note

**Priority:** critical

> As a logged-in user, I want to create a new note, so that I can capture my thoughts.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | I am logged in | I choose to create a new note | a new empty note opens ready for editing and appears in my notes list |
| AC-010 | I have created a new note without typing a title | the note is saved | it is given a sensible default or derived title so it can be identified in the list |

### US-006: Edit note content with rich text formatting

**Priority:** critical

> As a logged-in user, I want to format my note with headings, bold/italic, lists and checkboxes, so that my notes are structured and readable.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | I am editing a note | I apply a heading, bold, italic, a list or a checkbox to selected text | the formatting is applied and preserved when I reopen the note |
| AC-012 | I am editing a note containing a checkbox item | I tick or untick the checkbox | the checked state is saved and shown when I reopen the note |
| AC-013 | I am editing a note | I attempt to embed an image or attach a file | the app does not provide that capability in this version |

### US-007: Auto-save changes while editing

**Priority:** critical

> As a logged-in user, I want my edits to be saved automatically, so that I never lose work by forgetting to save.

| ID | Given | When | Then |
|---|---|---|---|
| AC-014 | I am editing a note | I pause or stop typing | my changes are saved automatically without me taking any action and the note's last-edited time updates |
| AC-015 | I have made edits that have been auto-saved | I close and reopen the note | my latest changes are present |
| AC-016 | I am editing a note | a save is in progress or has just completed | the app indicates the save status so I know my work is stored |

## EPIC-003: Organising Notes into Folders

Users organise notes into folders/notebooks and can rename notes and move them between folders. The notes list shows note titles with their last-edited time.

### US-008: Browse notes list with titles and last-edited time

**Priority:** high

> As a logged-in user, I want to see a list of my notes showing their titles and when each was last edited, so that I can quickly find and recognise the note I want.

| ID | Given | When | Then |
|---|---|---|---|
| AC-017 | I have notes in my account | I open the notes list | each note is shown with its title and last-edited time |
| AC-018 | I am viewing the notes list | a note's content changes and auto-saves | its last-edited time updates to reflect the most recent edit |

### US-009: Create and manage folders/notebooks

**Priority:** high

> As a logged-in user, I want to create folders/notebooks, so that I can group related notes together.

| ID | Given | When | Then |
|---|---|---|---|
| AC-019 | I am logged in | I create a folder and give it a name | the folder appears in my list of folders |
| AC-020 | I have a folder | I open it | I see only the notes that belong to that folder |

### US-010: Move a note between folders

**Priority:** medium

> As a logged-in user, I want to move a note from one folder to another, so that I can reorganise my notes as my needs change.

| ID | Given | When | Then |
|---|---|---|---|
| AC-021 | I have a note in one folder | I move it to another folder | the note appears in the destination folder and no longer in the original folder |

### US-011: Rename a note

**Priority:** medium

> As a logged-in user, I want to rename a note, so that its title reflects its content.

| ID | Given | When | Then |
|---|---|---|---|
| AC-022 | I have a note | I change its title | the new title is saved and shown in the notes list |

## EPIC-004: Full-text Search

Users find notes through a search box that searches across the content and titles of their notes.

### US-012: Search across my notes

**Priority:** high

> As a logged-in user, I want to search across the titles and content of my notes, so that I can find a note without browsing folders.

| ID | Given | When | Then |
|---|---|---|---|
| AC-023 | I have notes containing a particular word | I type that word into the search box | the matching notes are listed |
| AC-024 | I run a search | no notes match my query | I am shown a clear empty-result message |
| AC-025 | I am viewing search results | I select a result | the corresponding note opens |
| AC-026 | I run a search | results are returned | only notes belonging to my own account are included |

## EPIC-005: Delete, Trash & Restore Notes

Users can delete notes. Deleted notes go to a trash where they can be restored.

Assumption: The open understanding specifies delete with restore via a trash; the MVP scope lists 'delete notes'. Deleting is implemented as a recoverable trash/restore so users can undo accidental deletion.

### US-013: Delete a note to trash

**Priority:** high

> As a logged-in user, I want to delete a note I no longer need, so that my notes list stays uncluttered.

| ID | Given | When | Then |
|---|---|---|---|
| AC-027 | I have a note | I delete it | it is removed from my active notes list and moved to the trash |

### US-014: Restore a deleted note

**Priority:** medium

> As a logged-in user, I want to restore a note from the trash, so that I can recover from accidental deletion.

| ID | Given | When | Then |
|---|---|---|---|
| AC-028 | I have a note in the trash | I restore it | it returns to my active notes with its content and formatting intact |
| AC-029 | I am viewing the trash | I permanently delete a note from the trash | the note is removed and no longer recoverable |

## EPIC-006: Cross-device Sync & Offline (PWA)

The app is an installable Progressive Web App. Notes sync across the user's devices via the cloud, and the app works offline: users can read and edit notes without internet, and changes sync when they reconnect.

Assumption: Offline support is delivered as a PWA with service-worker caching and background sync on reconnect — not a native mobile or desktop app.

### US-015: Sync notes across devices

**Priority:** critical

> As a logged-in user with more than one device, I want my notes to sync across my devices via the cloud, so that I see the same up-to-date notes everywhere I log in.

| ID | Given | When | Then |
|---|---|---|---|
| AC-030 | I am logged in on two devices with internet access | I create or edit a note on one device | the change appears on the other device after syncing |

### US-016: Install the app as a PWA

**Priority:** medium

> As a logged-in user, I want to install the app to my device from the browser, so that I can open it like an app and use it offline.

| ID | Given | When | Then |
|---|---|---|---|
| AC-031 | I am using a supported browser | I choose to install the app | it is added to my device and can be launched as a standalone app |

### US-017: Read and edit notes offline

**Priority:** high

> As a logged-in user without internet, I want to read and edit my notes offline, so that I can keep working without a connection.

| ID | Given | When | Then |
|---|---|---|---|
| AC-032 | I have previously loaded my notes and then lost internet connection | I open the app offline | I can read my cached notes and make edits |
| AC-033 | I am offline and have edited a note | the edit is made | my changes are stored locally so they are not lost |

### US-018: Sync offline changes on reconnect

**Priority:** high

> As a logged-in user who edited offline, I want my offline changes to sync automatically when I reconnect, so that my notes stay consistent across devices without manual effort.

| ID | Given | When | Then |
|---|---|---|---|
| AC-034 | I made changes while offline | my device regains internet connection | my changes are synced to the cloud via background sync without me having to trigger it manually |
| AC-035 | the same note was changed offline on one device and separately in the cloud | my offline changes sync on reconnect | the app resolves the two versions without silently losing my data |
<!-- sdlc:auto:end epics -->
