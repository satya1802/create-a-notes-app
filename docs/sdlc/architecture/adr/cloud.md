<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-11-05

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Google Cloud
- Azure

## Decision Outcome

Chosen option: AWS, because Hosts the API (App Runner), database (RDS PostgreSQL 16 with backups and encryption) and integrates email in one account, with reliable always-on hosting for cross-device sync and room to grow.

## Consequences

More service choices to manage than an all-in-one PaaS, but keeps cost low at modest scale and avoids re-platforming later.
<!-- sdlc:auto:end adr -->