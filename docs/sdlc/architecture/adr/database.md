<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-11-05

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Stores the relational accounts/notes/folders/trash model with last-edited timestamps and serves the search box directly through built-in full-text (tsvector/GIN), avoiding a separate search engine.

## Consequences

Full-text search is good but less feature-rich than a dedicated engine; ample for a single-user personal notes corpus (NFR-012).
<!-- sdlc:auto:end adr -->