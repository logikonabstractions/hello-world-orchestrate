# PLAN

## Stage 0 — Dockerized local stack

### 0.1 — SQLite DB instance on Docker

- Objective:
  - Run SQLite in a container with persistent storage for local development.
- Deliverables:
  - `Dockerfile.sqlite`
  - `vibeCoding/SQLITE_DOCKER.md`
- Acceptance:
  - [x] SQLite image builds locally.
  - [x] Data persists across container restart via named volume.
- Demo commands:
  - `docker build -t hello-world-sqlite -f Dockerfile.sqlite .`
  - `docker exec hello-world-sqlite sqlite3 /data/app.db "SELECT id, value, created_at FROM submissions;"`
- Evidence:
  - Checkpoint 0.1 merged and validated by human.

### 0.2 — Front-end app on Docker

- Objective:
  - Run the Vite/Vue front-end as a containerized service for local demos.
- Deliverables:
  - `Dockerfile.frontend`
  - `vibeCoding/FRONTEND_DOCKER.md`
- Acceptance:
  - [ ] Front-end image builds successfully.
  - [ ] Container serves the built app on port `4173`.
  - [ ] Runbook includes build, run, and cleanup commands.
- Demo commands:
  - `docker build -t hello-world-frontend -f Dockerfile.frontend .`
  - `docker run --rm -p 4173:4173 hello-world-frontend`
- Evidence:
  - Command outputs from `npm run build` and Docker build/run logs.
