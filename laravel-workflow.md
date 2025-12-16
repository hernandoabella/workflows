🐘 Laravel Workflow
# 🐘 Laravel Workflow

A standardized workflow for developing, testing, and deploying Laravel applications.

---

## 1️⃣ Prerequisites

- PHP 8.2+
- Composer
- Node.js & npm
- MySQL / PostgreSQL
- Docker (recommended)
- Git

---

## 2️⃣ Project Setup

```bash
composer create-project laravel/laravel my-app
cd my-app
cp .env.example .env
php artisan key:generate


Install frontend dependencies (if needed):

npm install
npm run dev

3️⃣ Environment Configuration
.env (example)
APP_NAME=Laravel
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=app_db
DB_USERNAME=app_user
DB_PASSWORD=secret


Never commit .env files.

4️⃣ Git Workflow (Laravel-Specific)

main → production

develop → integration

feature/* → new features

fix/* → bug fixes

git checkout -b feature/user-auth

5️⃣ Database Workflow

Run migrations:

php artisan migrate


Seed data:

php artisan db:seed


Rollback safely:

php artisan migrate:rollback

6️⃣ Docker Workflow (Recommended)
docker-compose.yml (Laravel)
version: "3.9"

services:
  app:
    build: .
    container_name: laravel_app
    volumes:
      - .:/var/www/html
    ports:
      - "8000:8000"
    depends_on:
      - db
    command: php artisan serve --host=0.0.0.0 --port=8000

  db:
    image: mysql:8.0
    container_name: laravel_db
    environment:
      MYSQL_DATABASE: app_db
      MYSQL_USER: app_user
      MYSQL_PASSWORD: secret
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - db_data:/var/lib/mysql
    ports:
      - "3306:3306"

volumes:
  db_data:


Run:

docker compose up --build

7️⃣ Testing Workflow

Run all tests:

php artisan test


Specific test:

php artisan test --filter UserTest


Use a separate testing database.

8️⃣ Code Quality

Recommended tools:

Laravel Pint

PHPStan

Psalm

./vendor/bin/pint

9️⃣ Artisan Essentials
php artisan make:model Post -mcr
php artisan route:list
php artisan config:clear
php artisan cache:clear
php artisan optimize

🔐 Security Best Practices

Use environment variables

Hash passwords (Hash::make)

Validate all inputs

Use policies & gates

Enable CSRF protection

🚀 Deployment Workflow
Typical Flow
Local Development
   ↓
Git Push
   ↓
CI (tests, lint)
   ↓
Build Assets
   ↓
Deploy (EC2 / Forge / Vapor / Docker)

Production Commands
composer install --no-dev --optimize-autoloader
php artisan migrate --force
php artisan config:cache
php artisan route:cache
php artisan view:cache

🔁 Rollback Strategy

Database backups before deploy

Git tags for releases

Versioned releases

git tag v1.2.0
git push --tags

📦 Common Laravel Stacks
Stack	Use Case
Laravel + MySQL	Standard apps
Laravel + Redis	High performance
Laravel + Vue / React	SPA
Laravel + Inertia	Modern monolith
Laravel + API	Mobile / frontend apps
📌 Best Practices

Skinny controllers, fat services

Use Form Requests

Avoid logic in views

Queue long jobs

Log everything important
