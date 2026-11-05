<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-11-05

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- Express
- Django REST Framework

## Decision Outcome

Chosen option: FastAPI 0.115, because A lightweight Python API that cleanly covers sign-up, JWT-protected per-user access and batched sync endpoints, keeping a free consumer app cheap to run and quick to extend.

## Consequences

Async-first style and manual choice of auth/email libraries versus a batteries-included framework; fine for this modest surface.
<!-- sdlc:auto:end adr -->