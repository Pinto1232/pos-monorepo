# CI/CD Pipeline Documentation

This document describes the Continuous Integration and Continuous Deployment (CI/CD) pipeline for the POS system.

## Overview

The CI/CD pipeline is implemented using GitHub Actions and consists of the following jobs:

1. **Backend Build & Test**: Builds and tests the .NET backend application
2. **Frontend Build & Test**: Builds and tests the Next.js frontend application
3. **Docker Compose Test**: Tests the complete application stack using Docker Compose

## Pipeline Workflow

### Triggers

The pipeline is triggered on:
- Push to the `main` branch (affecting frontend, backend, or docker-compose.yml)
- Pull requests (affecting frontend, backend, or docker-compose.yml)

### Backend Job

The backend job performs the following steps:
1. Sets up PostgreSQL and Keycloak services for integration tests
2. Checks out the code
3. Caches NuGet packages
4. Sets up .NET 8.0
5. Runs .NET code analysis
6. Restores dependencies
7. Builds the backend
8. Runs security scanning
9. Runs tests with coverage reporting
10. Uploads build artifacts
11. Builds and pushes Docker image (only on main branch)

### Frontend Job

The frontend job performs the following steps:
1. Checks out the code
2. Caches Node modules
3. Sets up Node.js 18
4. Installs dependencies
5. Runs ESLint
6. Runs security scanning
7. Runs tests with coverage reporting
8. Builds the frontend
9. Uploads build artifacts
10. Builds and pushes Docker image (only on main branch)
11. Deploys to Vercel (only on main branch)

### Docker Compose Test Job

The Docker Compose test job performs the following steps:
1. Checks out the code
2. Installs Docker Compose
3. Builds and starts the Docker Compose environment
4. Waits for services to be ready
5. Runs basic integration tests
6. Cleans up the Docker Compose environment

## Environment Variables and Secrets

The pipeline uses the following GitHub Secrets:
- `DOCKERHUB_USERNAME`: DockerHub username for pushing images
- `DOCKERHUB_PASSWORD`: DockerHub password for pushing images
- `VERCEL_TOKEN`: Vercel token for deploying the frontend
- `SNYK_TOKEN`: Snyk token for security scanning (optional)

## Docker Images

The pipeline builds and pushes the following Docker images:
- `{DOCKERHUB_USERNAME}/pos-backend:latest`
- `{DOCKERHUB_USERNAME}/pos-backend:{COMMIT_SHA}`
- `{DOCKERHUB_USERNAME}/pos-frontend:latest`
- `{DOCKERHUB_USERNAME}/pos-frontend:{COMMIT_SHA}`

## Test Coverage

Test coverage reports are generated for both the backend and frontend and uploaded to Codecov.

## Artifacts

Build artifacts are retained for 7 days and include:
- Backend build output
- Frontend build output

## Local Development with Docker Compose

You can run the entire stack locally using Docker Compose:

```bash
docker-compose up -d --build
```

This will start the following services:
- Frontend: http://localhost:3000
- Backend: http://localhost:5107
- Keycloak: http://localhost:8282
- PostgreSQL: localhost:5432

## Troubleshooting

If you encounter issues with the CI/CD pipeline:

1. Check the GitHub Actions logs for detailed error messages
2. Verify that all required secrets are configured
3. Test the Docker Compose setup locally
4. Ensure health check endpoints are working correctly
