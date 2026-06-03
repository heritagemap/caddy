# AGENTS.md

## What this repo is

A minimal Docker image packaging a Caddy reverse-proxy config for `heritagemap.ru`. No application code lives here.

## Local verification

The only local check is building the image:

```bash
docker build --tag image .
```

There are no tests, linters, or typecheckers.

## Deployment

- Triggered on push to **`master`** or tags matching **`v*`**.
- GitHub Actions builds and pushes to the **legacy** GitHub Packages registry `docker.pkg.github.com`.
- The deploy job SSHs to a remote host, pulls the image, and runs it on the **`heritagemap`** Docker network.
- The container expects an upstream service **`frontend-pwa:9000`** reachable on that network.

## Key files

- `Caddyfile` — reverse-proxy rules and TLS config.
- `Dockerfile` — pins `caddy:2.7.6-alpine` and copies the config in.
