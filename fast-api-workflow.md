⚡ FastAPI Workflow
# ⚡ FastAPI Workflow

A standardized workflow for developing, testing, and deploying FastAPI applications.

---

## 1️⃣ Prerequisites

- Python 3.10+
- pip / poetry
- Git
- Docker (optional but recommended)
- uvicorn (ASGI server)
- Optional: Postgres / MySQL / SQLite

---

## 2️⃣ Project Setup

```bash
mkdir fastapi-app && cd fastapi-app
python -m venv venv
source venv/bin/activate
pip install fastapi uvicorn
pip install pydantic sqlalchemy alembic


Basic main.py:

from fastapi import FastAPI

app = FastAPI()

@app.get("/health")
def health_check():
    return {"status": "ok"}


Run dev server:

uvicorn main:app --reload

3️⃣ Environment Configuration
.env Example
ENV=development
DATABASE_URL=sqlite:///./app.db
SECRET_KEY=change_me


Never commit .env.

4️⃣ Folder Structure (Recommended)
fastapi-app/
├── app/
│   ├── api/
│   ├── core/
│   ├── db/
│   ├── models/
│   ├── schemas/
│   ├── services/
│   └── main.py
├── tests/
├── requirements.txt
├── Dockerfile
└── docker-compose.yml

5️⃣ Database Workflow

Use SQLAlchemy / Tortoise ORM

Migration: Alembic

alembic init alembic
alembic revision --autogenerate -m "initial"
alembic upgrade head

6️⃣ Docker Workflow
Dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]

docker-compose.yml
version: "3.9"

services:
  app:
    build: .
    ports:
      - "8000:8000"
    env_file:
      - .env
    volumes:
      - .:/app
    restart: unless-stopped

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: fastapi_db
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:

7️⃣ Testing Workflow

Install testing tools:

pip install pytest httpx pytest-asyncio


Run tests:

pytest


Best practices:

Separate test database

Test async endpoints

Use fixtures for setup/teardown

8️⃣ Code Quality

black (formatter)

flake8 (linter)

isort (import sorting)

mypy (type checking)

black .
flake8 .
isort .
mypy .

9️⃣ Security Best Practices

Validate inputs (Pydantic models)

JWT authentication

HTTPS in production

Environment variables for secrets

Rate limiting (via Starlette middleware or FastAPI plugins)

🔁 Deployment Workflow
Production Server

Gunicorn + Uvicorn Workers

Docker or Kubernetes

Load balancing & HTTPS

Example Gunicorn command:

gunicorn -w 4 -k uvicorn.workers.UvicornWorker app.main:app

CI/CD Flow Example
Git Push
  ↓
Run Linter & Tests
  ↓
Build Docker Image
  ↓
Push to Registry
  ↓
Deploy to ECS / EC2 / Kubernetes

🔄 Rollback Strategy

Keep previous Docker image tags

Database backups

Git tags for release

docker pull my-app:previous

📌 Best Practices

Async wherever possible

Modular folder structure

Version your API (v1, v2)

Centralized exception handling

Logging and monitoring
