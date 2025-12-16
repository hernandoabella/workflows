🐍 Python Workflow
# 🐍 Python Workflow

A standardized workflow for developing, testing, and deploying Python applications.

---

## 1️⃣ Prerequisites

- Python 3.10+
- pip / pipx
- virtualenv or venv
- Git
- Docker (recommended)

---

## 2️⃣ Project Setup

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate


Install dependencies:

pip install -r requirements.txt

3️⃣ Environment Configuration
.env Example
ENV=development
DEBUG=true
DATABASE_URL=postgresql://user:pass@db:5432/app
SECRET_KEY=change_me


Never commit .env.

4️⃣ Git Workflow

main → production

develop → integration

feature/* → features

fix/* → bug fixes

git checkout -b feature/api-auth

5️⃣ Folder Structure (Recommended)
src/
├── app/
│   ├── api/
│   ├── core/
│   ├── services/
│   ├── models/
│   └── main.py
├── tests/
├── requirements.txt
└── pyproject.toml (optional)

6️⃣ Development Workflow

Run app:

python src/app/main.py


For APIs:

FastAPI → uvicorn

Flask → flask run

Django → manage.py runserver

7️⃣ Docker Workflow
Dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "src/app/main.py"]

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


Run:

docker compose up --build

8️⃣ Testing Workflow

Install tools:

pip install pytest pytest-cov


Run tests:

pytest


Coverage:

pytest --cov=src

9️⃣ Code Quality

Recommended:

black

flake8

isort

mypy

black .
flake8 .
isort .

🔐 Security Best Practices

Never hardcode secrets

Use environment variables

Validate inputs

Keep dependencies updated

Use virtual environments

🚀 Deployment Workflow
Typical Flow
Local Dev
  ↓
Git Push
  ↓
CI (lint + test)
  ↓
Build (Docker / Wheel)
  ↓
Deploy (EC2 / ECS / Lambda / VPS)

Production Commands
pip install -r requirements.txt
python -m compileall .


Use:

Gunicorn / Uvicorn

Supervisor / Systemd

Docker / Serverless

🔁 Rollback Strategy

Git tags

Previous Docker images

Versioned releases

git tag v1.0.0
git push --tags

📦 Common Python Stacks
Stack	Use Case
FastAPI	Modern APIs
Flask	Lightweight apps
Django	Full-stack apps
Python Scripts	Automation
Data Jobs	ETL / ML
📌 Best Practices

One virtualenv per project

Small modules

Explicit dependencies

Type hints

Logging over print
