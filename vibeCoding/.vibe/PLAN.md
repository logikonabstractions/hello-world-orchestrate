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
  - To be provided by the response
- Evidence:
  - Vue components and dark-theme styling implemented under `src/`.
  - `npm install` succeeded in the environment.
  - `npm run build` succeeded and produced production assets in `dist/`.

### 0.1 — <SQLite DB instance on docker>

- Objective:
  - Configure a dockerfile + commands to run an SQLite db locally
- Deliverables:
  - Dockerfile with required configuration for SQLite
  - Docker volume to persist the data entered into the DB
  - Docker commands to run the DB locally
  - Required commands/instruction to add some data to the DB and test that is it persisted accross launches
- Acceptance:
  - [x] The SQLite docker container runs without errors
  - [x] Data entered in the database is persisted accross runs of the docker container
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


### 0.2 — <Docker-compose configuration>

- Objective:
  - Provide a docker-compose configuration that launches both the frontend & the DB containers in one command
- Deliverables:
  - Docker-compose.yaml with any necessary configuration to successfully launche both the frontend & the db container in one command
  - The docker-compose command that launches the containers
  - Additional configurations required so that the docker volumes are persisted across launches (consistent with checkpoint 0.1)
- Acceptance:
  - [ ] The frontend launches and is accessible via `localhost:<port>`
  - [ ] The SQLite DB launches and runs without errors
  - [ ] Data in the DB is persisteda cross 2 launches
- Demo commands:
  - To be provided by the response
- Evidence:
  - Console output showing the data is persisted across launches
  - Console output showing the frontend is launched


### 0.0 — <Configuration to save input to SQLite>

- Objective:
  - Update project configuration so that hitting the submit button will save the content of the input field into the DB in a persistant manner
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
  - Console output showing the data is persisted across launches
