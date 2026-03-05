# PLAN

## How to use this file

- This is the **checkpoint backlog**.
- Each checkpoint must have: Objective, Deliverables, Acceptance, Demo commands, Evidence.
- Keep checkpoints small enough to complete in one focused iteration.

## Stage 0 — <Vues-js testrun>

### 0.0 — <Init Vues-js Hello World>

- Objective:
  - Write an initial Hello World! vues-js frontend to kickstart this project
- Deliverables:
  - A fully initialized Vues-js app according to up to date standard
  - A customized home page
  - The home page has a dark theme
  - The home is divided into relevant component
  - The home page contains a "Submit" button
  - The home page contains an input field
  - Clicking the submit button yields a pop with the content of the input field
- Acceptance:
  - [x] Page has a dark theme
  - [x] Clicking the submit button launches a pop with the input field's content as text
  - [x] Any commands for local installation & running the code is provided in the response
- Demo commands:
  - `npm install`
  - `npm run dev`
  - `npm run build`
- Evidence:
  - Vue components and dark-theme styling implemented under `src/`.
  - `npm install` and `npm run build` succeeded.

### 0.1 — <SQLite DB instance on docker>

- Objective:
  - Configure a dockerfile + commands to run an SQLite db locally
- Deliverables:
  - Dockerfile with required configuration for SQLite
  - Docker volume to persist the data entered into the DB
  - Docker commands to run the DB locally
  - Required commands/instruction to add some data to the DB and test that it is persisted across launches
- Acceptance:
  - [x] The SQLite docker container runs without errors
  - [x] Data entered in the database is persisted across runs of the docker container
- Demo commands:
  - `docker build -t hello-world-sqlite -f Dockerfile.sqlite .`
  - `docker volume create hello_world_sqlite_data`
  - `docker run -d --name hello-world-sqlite -v hello_world_sqlite_data:/data hello-world-sqlite`
  - `docker exec hello-world-sqlite sqlite3 /data/app.db "CREATE TABLE IF NOT EXISTS submissions (id INTEGER PRIMARY KEY AUTOINCREMENT, value TEXT NOT NULL, created_at TEXT NOT NULL DEFAULT CURRENT_TIMESTAMP); INSERT INTO submissions(value) VALUES ('first launch value');"`
  - `docker exec hello-world-sqlite sqlite3 /data/app.db "SELECT id, value, created_at FROM submissions;"`
  - `docker rm -f hello-world-sqlite && docker run -d --name hello-world-sqlite -v hello_world_sqlite_data:/data hello-world-sqlite`
  - `docker exec hello-world-sqlite sqlite3 /data/app.db "SELECT id, value, created_at FROM submissions;"`
- Evidence:
  - Docker artifacts and step-by-step commands documented in `Dockerfile.sqlite` and `vibeCoding/SQLITE_DOCKER.md`.
  - Human validation confirmed container execution succeeds and inserted rows persist across relaunches.

### 0.1.2 — <Frontend config on docker>

- Objective:
  - Configure a dockerfile to run the frontend from the container
- Deliverables:
  - Dockerfile with required configuration for the vues-js app
  - The container must expose a port for use on localhost (e.g. `localhost:<port>`)
  - Provide relevant command to launch the container
- Acceptance:
  - [x] The container launch command and runbook are provided and validated for the production build path
  - [x] The frontend container is configured to be reachable at `localhost:4173`
- Demo commands:
  - `docker build -t hello-world-frontend -f Dockerfile.frontend .`
  - `docker run --rm --name hello-world-frontend -p 4173:4173 hello-world-frontend`
  - `curl -I http://localhost:4173`
- Evidence:
  - `Dockerfile.frontend` and `vibeCoding/FRONTEND_DOCKER.md` added for containerized frontend build/run.
  - `package-lock.json` added so Docker build can use `npm ci` reliably.
  - Frontend Docker image switched to Debian (`node:22-bookworm-slim`) to avoid Alpine musl Rollup optional-dependency failures.

### 0.2 — <Docker-compose configuration>

- Objective:
  - Provide a docker-compose configuration that launches both the frontend & the DB containers in one command
- Deliverables:
  - Docker-compose.yaml with any necessary configuration to successfully launch both the frontend & the db container in one command
  - The docker-compose command that launches the containers
  - Additional configurations required so that the docker volumes are persisted across launches (consistent with checkpoint 0.1)
- Acceptance:
  - [ ] The frontend launches and is accessible via `localhost:<port>`
  - [ ] The SQLite DB launches and runs without errors
  - [ ] Data in the DB is persisted across 2 launches
- Demo commands:
  - To be provided by the response
- Evidence:
  - Pending implementation in this repository.

### 0.3 — <Configuration to save input to SQLite>

- Objective:
  - Update project configuration so that hitting the submit button will save the content of the input field into the DB in a persistent manner
- Deliverables:
  - Updated configuration for Dockerfile, Docker-compose.yaml
  - Updated `Submit` button component that sends data to the SQLite db (instead of the popup, see checkpoint 0.0)
  - The content of the input field saved to the DB is persisted across launches
- Acceptance:
  - [ ] Checkpoint 0.2 still meets acceptance (e.g. do not break existing configurations)
  - [ ] Text entered into the input field is saved to the DB after hitting the `Submit` button
  - [ ] The content saved to the DB is persisted across launches
- Demo commands:
  - To be provided by the response
- Evidence:
  - Pending implementation in this repository.
