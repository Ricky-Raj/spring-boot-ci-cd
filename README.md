# Spring Boot CI/CD with GitHub Actions & Docker

A minimal Java Spring Boot app with an end-to-end CI/CD pipeline:
- Build & test with Maven
- Build Docker image
- Push to Docker Hub
- Deploy locally via Docker or docker-compose

## Prerequisites
- Git, Docker Desktop
- GitHub account + Docker Hub account

## Local build (no Maven installed? use Dockerized Maven)
```bash
# Build JAR using Maven in a container
docker run --rm -v "$PWD":/app -w /app maven:3.9.6-eclipse-temurin-17 mvn -B clean package

# Build image locally
docker build -t spring-boot-ci-cd:local .

# Run locally
docker run -p 8080:8080 spring-boot-ci-cd:local
# Open http://localhost:8080/
```

## docker-compose (pull image from Docker Hub)
1. Create a `.env` file with your Docker Hub username:
```
DOCKERHUB_USERNAME=your-username
```
2. Run:
```bash
docker compose up -d
```

## GitHub Actions setup
1. Create a new GitHub repo and push this project.
2. In **Settings → Secrets and variables → Actions → New repository secret**, add:
   - `DOCKERHUB_USERNAME` = your Docker Hub username
   - `DOCKERHUB_TOKEN` = a Docker Hub access token
3. Push/merge to `main` branch to trigger the workflow.
4. Image will be pushed to `docker.io/<username>/spring-boot-ci-cd:latest`.

## Endpoints
- `GET /` → `Hello, DevOps from Java 🚀`

## Screenshots to capture (for your report)
- Successful GitHub Actions run
- Docker Hub repository with the pushed image
- Local browser hitting `http://localhost:8080/`
(Triggered again for testing ??) 
