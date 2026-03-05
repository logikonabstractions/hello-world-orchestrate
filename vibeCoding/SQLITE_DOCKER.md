# Checkpoint 0.1 — SQLite DB instance on Docker

## Build the image

```bash
docker build -t hello-world-sqlite -f Dockerfile.sqlite .
```

## Create persistent volume

```bash
docker volume create hello_world_sqlite_data
```

## Start container

```bash
docker run -d --name hello-world-sqlite \
  -v hello_world_sqlite_data:/data \
  hello-world-sqlite
```

## Initialize schema and insert sample data

```bash
docker exec hello-world-sqlite sqlite3 /data/app.db "
CREATE TABLE IF NOT EXISTS submissions (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  value TEXT NOT NULL,
  created_at TEXT NOT NULL DEFAULT CURRENT_TIMESTAMP
);
INSERT INTO submissions(value) VALUES ('first launch value');
"
```

## Read data

```bash
docker exec hello-world-sqlite sqlite3 /data/app.db "SELECT id, value, created_at FROM submissions;"
```

## Verify persistence across container relaunch

```bash
docker rm -f hello-world-sqlite

docker run -d --name hello-world-sqlite \
  -v hello_world_sqlite_data:/data \
  hello-world-sqlite

docker exec hello-world-sqlite sqlite3 /data/app.db "SELECT id, value, created_at FROM submissions;"
```

## Cleanup (optional)

```bash
docker rm -f hello-world-sqlite
docker volume rm hello_world_sqlite_data
```
