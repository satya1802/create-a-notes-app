# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `6c2eeb0` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
This is a generated notes-app scaffold with two independent apps in one repo: a Vite + React 19 SPA (frontend/) whose screens were design-approved and currently run entirely on seeded sample data, and a FastAPI 0.115 service (backend/) that has no approved architecture yet and so only exposes a /health endpoint, backed by SQLAlchemy models and a SQLite database by default (switchable to Postgres via DATABASE_URL, with a docker-compose Postgres service provided for later use).
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for Vite 6 / React 19 / npm scripts in frontend/package.json)
- Python 3.12 (matches backend/Dockerfile base image)
- pip
- Docker and Docker Compose (optional, for the Postgres service in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. git clone the repository and cd into it
2. cd frontend && npm install
3. cd backend && pip install -r requirements.txt
4. (optional) docker compose up -d db  # starts Postgres 16 if you want to point DATABASE_URL at it instead of the default SQLite file
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| frontend dev | `cd frontend && npm run dev` | Starts the Vite dev server for the React SPA (default http://localhost:5173) |
| frontend build | `cd frontend && npm run build` | Bundles the frontend app (does not typecheck) |
| frontend preview | `cd frontend && npm run preview` | Serves the production build locally |
| backend dev | `cd backend && uvicorn app.main:app --reload` | Runs the FastAPI service with auto-reload; creates SQLite tables on startup and serves /health |
| db up | `docker compose up -d db` | Starts the Postgres 16 container defined in docker-compose.yml |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `.devcontainer` | Dev container configuration for a consistent development environment |
| `.quorq` | Platform metadata (handoff.json) used by the Quorq AI SDLC platform |
| `backend` | FastAPI service: app/, tests/, Dockerfile, requirements.txt, lint/test config |
| `backend/app` | Application code: main.py (entrypoint/CORS/health), database.py (engine/session), models.py (SQLAlchemy models, currently empty), schemas.py (Pydantic models/StubResponse), routers/ (one router per architecture component, currently empty) |
| `backend/tests` | Pytest tests (conftest.py fixtures, test_health.py) run against the FastAPI app |
| `frontend` | Vite + React 19 SPA: src/, e2e/, config files for Vite, TypeScript, ESLint, Prettier, Playwright |
| `frontend/src` | Application source: main.tsx entrypoint, lib/ (api.ts client, ui.tsx, icons.tsx, navigate.ts), index.css, test-setup.ts |
| `frontend/e2e` | Playwright end-to-end spec files (e.g. example.spec.ts) |
| `docker-compose.yml` | Defines the optional Postgres 16 database service for local development |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend: one router per architecture component under app/routers/, imported into main.py; routes are generated as typed stubs returning schemas.StubResponse until implemented
- Backend: all SQLAlchemy models inherit app.database.Base, imported in main.py before create_all so tables register on startup (no migrations yet)
- Backend: request-scoped DB sessions via the get_db dependency generator in database.py
- Backend: DATABASE_URL env var selects the database (defaults to local SQLite file app.db); ALLOWED_ORIGINS env var (comma-separated) configures CORS, falling back to the Vite dev server origins
- Frontend: one module per approved screen expected under src/screens/ (per frontend/README), with App.tsx as the navigation shell/route table
- Frontend: shared component/icon vocabulary in src/lib/ui.tsx and src/lib/icons.tsx; API access centralized in src/lib/api.ts via apiFetch, using VITE_API_BASE_URL and a bearer token (VITE_API_SECRET_KEY or a stored session token)
- Frontend: component tests live beside the components they test and are collected only from src/**/*.{test,spec}.{ts,tsx} by Vitest; Playwright specs live in e2e/ and are run separately
- Screens currently render seeded sample data rather than calling the backend; wiring to real endpoints is explicitly left as future work
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| backend test | `cd backend && pytest` | Runs the backend test suite (pythonpath=. so tests can import app) |
| backend lint | `cd backend && ruff check .` | Lints the backend code with Ruff |
| backend format | `cd backend && ruff format .` | Formats backend code with Ruff |
| frontend test | `cd frontend && npm run test` | Runs Vitest component tests |
| frontend lint | `cd frontend && npm run lint` | Runs ESLint over the frontend app |
| frontend typecheck | `cd frontend && npm run typecheck` | Runs tsc --noEmit to typecheck the frontend |
| frontend e2e install | `cd frontend && npm run test:e2e:install` | Installs the Chromium browser needed by Playwright |
| frontend e2e | `cd frontend && npm run test:e2e` | Runs Playwright acceptance tests from e2e/; builds/serves the app and starts the backend locally unless E2E_BASE_URL is set |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend screens don't show data from the backend | Expected: generated screens render seeded sample data only; the backend currently only implements /health. Wiring a screen to a real endpoint is the next task, per src/lib/api.ts and the READMEs. |
| CORS errors when the frontend calls the backend | Set the ALLOWED_ORIGINS env var on the backend to the frontend's origin (comma-separated for multiple); by default only http://localhost:5173 and http://127.0.0.1:5173 are allowed. |
| `npm run build` succeeds but `tsc` fails elsewhere | `npm run build` does not typecheck; run `npm run typecheck` (tsc --noEmit) to catch type errors before relying on them being caught by the build. |
| Playwright e2e tests fail to start the backend | The Playwright config expects a Python virtualenv at backend/.venv with dependencies installed (backend/.venv/bin/python -m uvicorn ...); create it and `pip install -r backend/requirements.txt` into it, or set E2E_BASE_URL to point at an already-running deployment instead. |
| Backend fails to connect to a database | By default DATABASE_URL is unset and the app uses a local SQLite file (sqlite:///./app.db), requiring no server. To use Postgres, run `docker compose up -d db` and set DATABASE_URL accordingly. |
<!-- sdlc:auto:end troubleshooting -->
