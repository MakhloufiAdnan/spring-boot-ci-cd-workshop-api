# Spring Boot CI/CD Workshop API

REST API for workshop management built with **Java 21, Spring Boot and PostgreSQL**.

The main engineering focus of this repository is the automation of the build, test, containerization and release lifecycle.

## 🛠️ Tech Stack

- Java 21
- Spring Boot 3.2.4
- PostgreSQL 16
- Gradle 8.7
- Docker / Docker Compose
- GitHub Actions
- GitHub Container Registry
- semantic-release
- Python automation scripts

## ⚙️ CI/CD Pipeline

The GitHub Actions workflow automates the main stages of the delivery process.

### Test

The pipeline:

- installs the required Java tooling
- executes automated tests
- collects JUnit XML reports
- publishes test results for CI analysis

Tests can also be executed through the repository automation script:

```bash
python run-tests.py
```

Or directly with Gradle:

./gradlew clean test
🐳 Docker

The backend uses a multi-stage Docker build:

Gradle + JDK 21 build stage
        ↓
Spring Boot application build
        ↓
Eclipse Temurin JRE 21 runtime

This keeps the final image focused on runtime dependencies.

PostgreSQL is started through Docker Compose and includes a health check before the application starts.

📦 Container Registry

Docker images are automatically published to GitHub Container Registry (GHCR).

The CI/CD workflow creates image tags associated with branches, commits and application releases.

🚀 Automated Releases

Releases from the main branch are managed with semantic-release.

The release workflow:

analyzes commit history
determines the next semantic version
creates a GitHub Release
updates the changelog
publishes a versioned Docker image

🗄️ Database

The application uses PostgreSQL 16.
Configuration is provided through Spring environment variables:

SPRING_DATASOURCE_URL
SPRING_DATASOURCE_USERNAME
SPRING_DATASOURCE_PASSWORD

▶️ Run Locally
Requirements
Java 21
Docker
Git

Compile:

./gradlew clean compileJava
Run the application:
./gradlew bootRun

API:
http://localhost:8080

🐳 Run with Docker Compose

Start the API and PostgreSQL:
docker compose up -d

Stop:
docker compose down
Remove containers and persistent development data:
docker compose down -v

📌 Project Focus

This repository demonstrates backend development and DevOps practices around a Spring Boot application:

REST API development
PostgreSQL integration
automated testing
reproducible Gradle builds
Docker containerization
CI/CD with GitHub Actions
automated semantic versioning
GitHub Releases
container publishing to GHCR
