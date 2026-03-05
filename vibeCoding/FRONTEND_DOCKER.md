# Checkpoint 0.2 — Front-end app on Docker

## Build the image

```bash
docker build -t hello-world-frontend -f Dockerfile.frontend .
```

## Run container

```bash
docker run --rm --name hello-world-frontend -p 4173:4173 hello-world-frontend
```

Then open: <http://localhost:4173>

## Smoke test with curl

```bash
curl -I http://localhost:4173
```

Expected status: `HTTP/1.1 200 OK`

## Stop and cleanup

With `--rm`, the container is removed automatically on stop.

If running detached (`-d`), stop manually:

```bash
docker stop hello-world-frontend
```


## Troubleshooting

If you encounter a Rollup optional dependency error on Alpine (for example missing `@rollup/rollup-linux-x64-musl`), this image uses Debian-based Node (`node:22-bookworm-slim`) to avoid that npm optional-dependency issue during `npm ci` + `npm run build`.
