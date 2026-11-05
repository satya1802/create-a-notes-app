<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-11-05

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue 3
- Svelte

## Decision Outcome

Chosen option: React 19, because Drives the state-heavy editing screen, auto-save status, live notes list and search, and anchors the installable PWA with service-worker offline caching and background sync, backed by mature rich-text and PWA libraries.

## Consequences

Requires selecting and wiring a rich-text editor and offline sync layer rather than getting them built in; delivered as a PWA (no native app shell).
<!-- sdlc:auto:end adr -->