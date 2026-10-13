# Runbook

> Fill in every TODO with exact commands. / Попълнете всяко TODO с точни команди.

## Start locally / Локално стартиране

python -m venv .venv
.venv\Scripts\activate
pip install -r requirements-dev.txt
uvicorn app.main:app --reload

## Check that it works / Проверка, че работи

http://127.0.0.1:9000/health

## Run the tests / Тестове

pytest
ruff check .

## When something breaks / Когато нещо се счупи

curl http://127.0.0.1:9000/health: работи ли процесът изобщо?
curl http://127.0.0.1:9000/ready: ако е 503, хранилището (базата) не се достига; проверете DATABASE_URL.
Прегледайте логовете в терминала, където работи uvicorn.
