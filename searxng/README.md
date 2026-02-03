# SearXNG (Docker Compose)

This directory contains a minimal, production-friendly SearXNG stack with:
- `searxng` service
- `valkey` for rate limiting
- `nginx` reverse proxy with Basic Auth and optional IP allowlist

## Quick Start

1. Configure `.env` and `settings.yml`.
2. Start the stack:

```bash
cd /Users/hiyenwong/projects/IdeaProjects/docker_hub/searxng
docker compose up -d
```

3. Open in browser:

- `http://localhost:8080` (or the port set in `.env`)

## Configuration

### .env

Key options:
- `HOST_PORT`: external port exposed on the host
- `SEARXNG_SECRET`: required, must be a long random string
- `SEARXNG_BASE_URL`: the public URL users will access
- `SEARXNG_VALKEY_URL`: valkey connection URL
- `BASIC_AUTH_REALM`: set to `off` to disable Basic Auth

### settings.yml

Basic server settings are provided. Adjust `public_instance`, `limiter`, and any other SearXNG options here.

## Basic Auth

Basic Auth is enabled by default through `nginx`.

Default credentials:
- user: `admin`
- password: `change-me`

Change the password:

```bash
openssl passwd -apr1 'your-new-password'
```

Then replace the password hash in `nginx/.htpasswd`:

```
admin:<hash-here>
```

Disable Basic Auth by setting `.env`:

```
BASIC_AUTH_REALM=off
```

## IP Allowlist (optional)

Edit `nginx/allowlist.conf`.

Default allows all IPs:

```
allow 0.0.0.0/0;
allow ::/0;
```

To restrict access:

```
allow 203.0.113.10/32;
allow 198.51.100.0/24;
deny all;
```

## Notes

- `searxng` listens on port `8080` internally and is only exposed via `nginx`.
- `valkey` is used for rate limiting and should remain enabled for public deployments.
