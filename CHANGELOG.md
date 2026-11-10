# Changelog

## 0.6.1

- `/version` reports 0.6.1 by default.

## 0.6.0

- CI pushes the image to GHCR (`:sha`, `:latest` on main, `:vX.Y.Z` on tags).
- Trivy blocks the push on fixable CRITICAL vulnerabilities.
- `compose.prod.yaml` pulls the image instead of building it (`APP_TAG`).
- Documentation is published to GitHub Pages.

## 0.4.0

- Run the app and PostgreSQL with Docker Compose (`docker compose up`).
- Notes are stored in PostgreSQL and survive restarts (named volume `db-data`).
- The app starts only after the database is healthy.
- Credentials come from `.env`; `.env.example` lists the variables.
- Optional Adminer on port 8081 with `--profile tools`.

## 0.2.0

- Initial template: notes API with health and version endpoints.
