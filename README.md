# Kittygram — сервис для публикации фотографий котиков

## Описание проекта

Kittygram — учебный проект, представляющий собой простое веб-приложение для публикации и просмотра фотографий котиков с кратким описанием. Пользователи могут зарегистрироваться, добавлять новых котиков с именем, цветом, описанием и фотографией, а также просматривать карточки других участников.

Проект реализован по классической трёхкомпонентной архитектуре:
- **фронтенд** (React SPA),
- **бэкенд** (Django REST API),
- **база данных** (PostgreSQL),
- весь трафик принимает **gateway** на базе Nginx.

## Стек технологий

- Python 3.11, Django 3.2, Django REST Framework, Gunicorn
- PostgreSQL 13
- React (Create React App), Node.js 18
- Nginx (как reverse proxy и раздача статики)
- Docker, Docker Compose
- CI/CD: GitHub Actions, Docker Hub
- Дополнительно: ruff (линтинг), pytest, pytest-django, psycopg2, Pillow

## Как развернуть проект локально

### 1. Клонировать репозиторий


git clone https://github.com/GOCTb/kittygram-final-ad.git
cd kittygram-final-ad

2. Создать файл .env
В корне проекта создайте файл .env и заполните его по образцу (пример в файле .env.example):

POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=your_secure_password
DJANGO_SECRET_KEY=generate_a_random_secret_key
DEBUG=False
ALLOWED_HOSTS=localhost,127.0.0.1
DB_HOST=db
DB_PORT=5432
Для генерации секретного ключа можно выполнить:

python3 -c "import secrets; print(secrets.token_urlsafe(50))"

3. Запустить контейнеры

docker compose up -d --build

4. Выполнить миграции и создать суперпользователя

docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py createsuperuser

5. Открыть в браузере
Фронтенд: http://localhost:8081

Админка: http://localhost:8081/admin/

6. Остановить контейнеры

docker compose down
CI/CD
При пуше в ветку main автоматически запускаются GitHub Actions:

Линтинг бэкенда ruff.

Тесты бэкенда и фронтенда.

Сборка Docker-образов kittygram_backend, kittygram_frontend, kittygram_gateway и их загрузка на Docker Hub.

Отправка уведомления в Telegram об успешном завершении.

Автор
GOCTb
