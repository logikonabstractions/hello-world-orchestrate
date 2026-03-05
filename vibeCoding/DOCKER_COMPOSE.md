# Checkpoint 0.2 — Docker Compose for frontend + SQLite

## Start both services

```bash
docker compose up -d --build
```

Frontend URL: <http://localhost:4173>

## Verify frontend is reachable

```bash
curl -I http://localhost:4173
```

Expected: `HTTP/1.1 200 OK`

## Verify SQLite container is running

```bash
docker compose ps
```

Look for service `sqlite` in `running` state.

## Initialize schema and insert data

```bash
docker compose exec sqlite sqlite3 /data/app.db "
CREATE TABLE IF NOT EXISTS submissions (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  value TEXT NOT NULL,
  created_at TEXT NOT NULL DEFAULT CURRENT_TIMESTAMP
);
INSERT INTO submissions(value) VALUES ('compose launch value');
"
```

## Confirm inserted rows

```bash
docker compose exec sqlite sqlite3 /data/app.db "SELECT id, value, created_at FROM submissions;"
```

## Verify persistence across relaunches

```bash
docker compose down

docker compose up -d

docker compose exec sqlite sqlite3 /data/app.db "SELECT id, value, created_at FROM submissions;"
```

If the previously inserted row still exists, persistence is working via the named volume `hello_world_sqlite_data`.

## Stop services

```bash
docker compose down
```

## Full cleanup (including persisted data)

```bash
docker compose down -v
```
