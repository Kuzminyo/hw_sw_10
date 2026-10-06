# Quotes to Scrape — Django

Аналог http://quotes.toscrape.com на Django + PostgreSQL.

## Можливості

- Реєстрація, вхід, вихід (`/users/register/`, `/users/login/`).
- Додавання автора та цитати (з тегами) — лише для зареєстрованих користувачів.
- Перегляд усіх цитат і сторінок авторів — без автентифікації.
- Пошук за тегом (`/tag/<name>/`), блок **Top Ten tags**, пагінація Next / Previous.
- Кнопка «Scrape quotes.toscrape.com» на головній (для залогінених) — скрапить сайт і наповнює БД.
- Міграція даних з MongoDB (ДЗ №9) у Postgres: `python manage.py migrate_from_mongo`.

## Запуск

```bash
pip install -r requirements.txt
cp .env.example .env          # підставте свої значення
docker compose up -d          # Postgres
python manage.py migrate
python manage.py createsuperuser   # за бажанням
python manage.py runserver
```

Якщо `POSTGRES_DB` у `.env` не задано — використовується SQLite (для швидкої перевірки).

## Наповнення бази

З MongoDB попереднього ДЗ (колекції `authors` і `quotes`, автор у цитаті — ObjectId або ім'я):

```bash
python manage.py migrate_from_mongo --uri mongodb://localhost:27017 --db quotes_db
```

Або скрапінгом — кнопкою на сайті чи командою:

```bash
python manage.py scrape_quotes
```