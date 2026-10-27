# Runbook

> Fill in every TODO with exact commands. / Попълнете всяко TODO с точни команди.

## Start locally / Локално стартиране

python -m venv .venv
.venv\Scripts\activate
pip install -r requirements-dev.txt
uvicorn app.main:app --reload

## Check that it works / Проверка, че работи

http://127.0.0.1:8000/health

## Run the tests / Тестове

pytest
ruff check .

## When something breaks / Когато нещо се счупи

curl http://127.0.0.1:8000/health: работи ли процесът изобщо?
curl http://127.0.0.1:8000/ready: ако е 503, хранилището (базата) не се достига; проверете DATABASE_URL.
Прегледайте логовете в терминала, където работи uvicorn.

## Стартиране с Docker / Run with Docker

Build:

    docker build -t notes-api:0.3.0 .

Run:

    docker run -d --name notes-api -p 8000:8000 notes-api:0.3.0

Check / Проверка: http://127.0.0.1:8000/health (в Codespaces: PORTS → 8000) и

    docker inspect --format '{{.State.Health.Status}}' notes-api

трябва да върне `healthy` (след около 15 секунди).

Logs / Логове:

    docker logs -f notes-api

Stop / Спиране:

    docker stop notes-api
    docker rm notes-api

## Стартиране с Compose / Run with Compose

Еднократно: копирайте `.env.example` като `.env` и сложете истинска парола. / Once: copy `.env.example` to `.env` and set a real password.

    copy .env.example .env

Start / Стартиране (приложение + PostgreSQL):

    docker compose up -d --build

Status / Състояние: `app` и `db` трябва да са `(healthy)`.

    docker compose ps

Check / Проверка: http://127.0.0.1:8000/ready трябва да върне `{"status":"ready"}`.

Logs / Логове:

    docker compose logs -f app
    docker compose logs db

Adminer (само при нужда, сървър: `db`): http://127.0.0.1:8081

    docker compose --profile tools up -d

Stop / Спиране:

    docker compose down

`down` спира и изтрива контейнерите и мрежата, но volume-ът `db-data` остава и бележките се пазят. / `down` removes containers and the network; the `db-data` volume stays, so notes survive.

    docker compose down -v

`down -v` изтрива и volume-а: **всички бележки се губят**. / `down -v` also deletes the volume: **all notes are lost**.
