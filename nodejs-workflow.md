# 🟢 Node.js Workflow

A standardized workflow for developing, testing, and deploying Node.js applications.

---

## 1️⃣ Prerequisites

- Node.js 18+
- npm / yarn / pnpm
- Git
- Docker (recommended)

---

## 2️⃣ Project Setup

```bash
mkdir my-app && cd my-app
npm init -y
npm install express
Basic server:

js
Copiar código
import express from "express";

const app = express();
app.use(express.json());

app.get("/health", (_, res) => res.json({ status: "ok" }));

app.listen(3000, () => console.log("Server running"));
3️⃣ Environment Configuration
.env Example
env
Copiar código
PORT=3000
NODE_ENV=development
DATABASE_URL=mysql://user:pass@db:3306/app
JWT_SECRET=change_me
Never commit .env.

4️⃣ Git Workflow
main → production

develop → integration

feature/* → features

fix/* → bug fixes

bash
Copiar código
git checkout -b feature/auth
5️⃣ Folder Structure (Recommended)
txt
Copiar código
src/
├── controllers/
├── routes/
├── services/
├── middlewares/
├── utils/
├── app.js
└── server.js
6️⃣ Development Workflow
Start dev server:

bash
Copiar código
npm run dev
Recommended tools:

nodemon / ts-node-dev

eslint + prettier

7️⃣ Docker Workflow
Dockerfile
Dockerfile
Copiar código
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

EXPOSE 3000

CMD ["npm", "run", "start"]
docker-compose.yml
yaml
Copiar código
version: "3.9"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    env_file:
      - .env
    volumes:
      - .:/app
      - /app/node_modules
    restart: unless-stopped
Run:

bash
Copiar código
docker compose up --build
8️⃣ Testing Workflow
Install:

bash
Copiar código
npm install --save-dev jest supertest
Run tests:

bash
Copiar código
npm test
Use separate test env:

env
Copiar código
NODE_ENV=test
DATABASE_URL=...
9️⃣ Code Quality
Recommended:

ESLint

Prettier

Husky

lint-staged

bash
Copiar código
npm run lint
npm run format
🔐 Security Best Practices
Validate inputs

Use Helmet

Rate limiting

Environment variables for secrets

Avoid eval

🚀 Deployment Workflow
Typical Flow
txt
Copiar código
Local Dev
  ↓
Git Push
  ↓
CI (lint + test)
  ↓
Build
  ↓
Deploy (Docker / EC2 / ECS / Railway / Render)
Production Start
bash
Copiar código
npm ci --only=production
npm run build
npm run start
Use:

PM2

Docker

Cloud provider services

🔁 Rollback Strategy
Git tags

Previous Docker images

Health checks

bash
Copiar código
git tag v1.0.0
git push --tags
📦 Common Node.js Stacks
Stack	Use Case
Express	Simple APIs
Fastify	High performance
NestJS	Enterprise apps
Node + GraphQL	APIs
Node + WebSockets	Real-time

📌 Best Practices
One responsibility per module

Async/await everywhere

Centralized error handling

Graceful shutdown

Structured logging
