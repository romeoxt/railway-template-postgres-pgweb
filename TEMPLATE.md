# Railway Template Composer Setup

## Marketplace listing

- **Title:** Deploy and Host PostgreSQL + PgWeb with Railway
- **Short description:** Postgres with a browser SQL client — browse tables and run queries without pgAdmin.
- **Category:** Storage
- **Overview:** paste `README.md`

## Services

| Service | Source | Volume | Public HTTP |
| --- | --- | --- | --- |
| PgWeb | GitHub repo (Dockerfile) | — | Yes |
| Postgres | Railway PostgreSQL plugin | `/var/lib/postgresql/data` | No |

## Variables — PgWeb

| Variable | Value | Secret | Description |
| --- | --- | --- | --- |
| `DATABASE_URL` | `${{Postgres.DATABASE_URL}}` | Yes | Postgres connection over private network |

## Settings — PgWeb

- Healthcheck: `/` (Dockerfile default)
- Keep Postgres private; only PgWeb is public
- Add security note in listing for production use
