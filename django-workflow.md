🟦 Django Workflow
# 🟦 Django Workflow

A standardized workflow for developing, testing, and deploying Django applications.

---

## 1️⃣ Prerequisites

- Python 3.10+
- pip / poetry
- Git
- Docker (optional but recommended)
- PostgreSQL / MySQL / SQLite

---

## 2️⃣ Project Setup

```bash
mkdir django-app && cd django-app
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install django djangorestframework psycopg2-binary
django-admin startproject myproject .


Run development server:

python manage.py runserver

3️⃣ Environment Configuration
.env Example
ENV=development
DEBUG=True
SECRET_KEY=change_me
DATABASE_URL=postgres://user:pass@db:5432/django_db


Never commit .env.

4️⃣ Git Workflow

main → production

develop → integration

feature/* → features

fix/* → bug fixes

git checkout -b feature/user-auth

5️⃣ Recommended Folder Structure
django-app/
├── myproject/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── apps/
│   ├── users/
│   └── products/
├── templates/
├── static/
├── tests/
├── requirements.txt
├── Dockerfile
└── docker-compose.yml

6️⃣ Database Workflow

Run migrations:

python manage.py makemigrations
python manage.py migrate


Create superuser:

python manage.py createsuperuser


Rollback migration:

python manage.py migrate appname previous_migration

7️⃣ Docker Workflow
Dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]

docker-compose.yml
version: "3.9"

services:
  web:
    build: .
    env_file:
      - .env
    ports:
      - "8000:8000"
    volumes:
      - .:/app
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: django_db
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:


Run:

docker compose up --build

8️⃣ Testing Workflow

Install testing tools:

pip install pytest pytest-django coverage


Run tests:

pytest


Check coverage:

pytest --cov=apps

9️⃣ Code Quality

black (formatter)

flake8 (linter)

isort (import sorting)

mypy (type checking)

black .
flake8 .
isort .
mypy .

🔐 Security Best Practices

Use environment variables

Enable CSRF and XSS protection

Use HTTPS in production

Hash passwords with Django’s auth system

Apply migrations before release

🚀 Deployment Workflow

Gunicorn + Nginx for production

Docker / Kubernetes recommended

Database migrations applied before start

Optional: AWS Elastic Beanstalk, ECS, or Heroku

Example Gunicorn command:

gunicorn myproject.wsgi:application --workers 4 --bind 0.0.0.0:8000

CI/CD Example
Git Push
  ↓
Run Linter & Tests
  ↓
Build Docker Image
  ↓
Push to Registry
  ↓
Deploy to ECS / EC2 / Kubernetes

🔁 Rollback Strategy

Keep previous Docker image tags

Backup database before deploy

Git tags for releases

docker pull django-app:previous

📌 Best Practices

Modular apps (one app per feature)

Use settings module per environment

Centralized logging

Use Django signals carefully

Keep requirements pinned
