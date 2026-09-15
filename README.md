# Deploy and Host PostgreSQL + PgWeb with Railway

Spin up Postgres with a browser-based SQL client — browse tables, run queries, and inspect data without installing pgAdmin locally.

## About PostgreSQL + PgWeb

This template pairs Railway PostgreSQL with [PgWeb](https://github.com/sosedoff/pgweb), a lightweight web UI for PostgreSQL. Postgres stays on the private network; PgWeb connects over `${{Postgres.DATABASE_URL}}` and exposes a public HTTPS URL for debugging and exploration.

## About Hosting PostgreSQL + PgWeb

Self-hosting your database on Railway gives you a persistent Postgres instance with a volume-backed data path, plus a UI you can open from any machine. Railway wires private networking between services so Postgres is never exposed to the public internet.

## Environment Variables

| Variable | Description | Secret | Example/Notes |
| --- | --- | --- | --- |
| `DATABASE_URL` | PostgreSQL connection for PgWeb | Yes | `${{Postgres.DATABASE_URL}}` |

Set `DATABASE_URL` on the **PgWeb** service only. Your app services use the same `${{Postgres.DATABASE_URL}}` reference to share the database.

## Deploy and Host

1. Create a new Railway project.
2. Add **PostgreSQL** and attach a **volume** at `/var/lib/postgresql/data`.
3. Deploy this repo as a second service named **PgWeb** (Dockerfile build).
4. Set `DATABASE_URL` = `${{Postgres.DATABASE_URL}}` on PgWeb.
5. Enable **public HTTP** on PgWeb only — keep Postgres private.
6. Deploy and open the PgWeb URL in your browser.
7. Point other services in the same project at `${{Postgres.DATABASE_URL}}` for your application database.

## Security note

PgWeb is public in this template for fast hackathon and MVP access. For production data, add authentication (proxy, IP allowlist, or Railway access controls) before storing real user information.

## Common Use Cases

- Hackathon databases with an instant browser UI
- MVP backends that need Postgres on day one
- Debugging schema and data during development
- Shared database for multiple Railway services in one project

## Dependencies for PostgreSQL + PgWeb Hosting

The Railway template includes:

- **PgWeb** — this repo (Dockerfile → `sosedoff/pgweb`)
- **PostgreSQL** — Railway PostgreSQL plugin with volume at `/var/lib/postgresql/data`

## Deployment Dependencies

- [PgWeb GitHub](https://github.com/sosedoff/pgweb)
- [Railway PostgreSQL docs](https://docs.railway.com/databases/postgresql)

## Why Deploy PostgreSQL + PgWeb on Railway?

Postgres provisioning, volume persistence, private networking, and a public database UI — all in one canvas. No local Docker Compose or VPN required to inspect your data.

## Template Content

| Service | Source |
| --- | --- |
| PgWeb | GitHub repo (Dockerfile) |
| Postgres | Railway PostgreSQL plugin |

## Run locally

```bash
docker build -t pgweb-local .
docker run -p 8081:8081 -e DATABASE_URL=postgres://user:pass@host:5432/db pgweb-local
```

## Marketing site

See `website/index.html` for the template landing page.

## Author

romeoxt — herbylegall9@gmail.com

## License

MIT
