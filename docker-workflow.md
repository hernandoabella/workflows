# 🐳 Docker Workflow

A standardized workflow to build, run, and manage applications using Docker.

## 1️⃣ Prerequisites

- Docker installed  
- Docker Compose (optional but recommended)
- Project includes:
  - `Dockerfile`
  - `.dockerignore` (recommended)

## 2️⃣ Project Structure

```txt
project-root/
├── Dockerfile
├── .dockerignore
├── docker-compose.yml (optional)
└── src/
```

## 3️⃣ Dockerfile Example

```Dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "run", "dev"]

```

## 4️⃣ Build the Image
```bash
docker build -t my-app .
```

## 5️⃣ Run the Container
```bash
docker run -p 3000:3000 my-app
```

Run in detached mode:

```bash
docker run -d -p 3000:3000 my-app
```

6️⃣ Using Docker Compose (Recommended)
docker-compose.yml

```yaml
version: "3.9"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    environment:
      - NODE_ENV=development
```

Start services:
```bash
docker compose up
```

Stop services:
```bash
docker compose down
```

7️⃣ Common Docker Commands
Command	Description
docker ps	List running containers
docker images	List images
docker logs <container>	View logs
docker exec -it <container> sh	Access container shell
docker system prune	Clean unused resources
8️⃣ Environment Variables

Use .env files:

PORT=3000
NODE_ENV=development


Docker Compose automatically loads .env.

9️⃣ Production Tips

Use multi-stage builds

Avoid mounting volumes in production

Use .dockerignore

Pin image versions (avoid latest)

Run containers as non-root

🔁 Reuse Pattern

This workflow can be duplicated and adapted for:

React / Next.js

Node.js APIs

Laravel / PHP

Python / FastAPI

Microservices

✅ Ready for CI/CD

Compatible with:

GitHub Actions

GitLab CI

Docker Hub

AWS / GCP / Azure

