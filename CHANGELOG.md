# Changelog

## 0.4.0

- Run the app and PostgreSQL with Docker Compose (`docker compose up`).
- Notes are stored in PostgreSQL and survive restarts (named volume `db-data`).
- The app starts only after the database is healthy.
- Credentials come from `.env`; `.env.example` lists the variables.
- Optional Adminer on port 8081 with `--profile tools`.

## 0.2.0

- Initial template: notes API with health and version endpoints.
