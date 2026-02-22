# Node.js CI/CD Pipeline with Docker & GitHub Actions

This repository demonstrates a complete end-to-end CI/CD pipeline for a simple Node.js HTTP application using Docker and GitHub Actions. The project follows a production-oriented approach with automated testing, image tagging, secure deployment, and post-deployment verification.

---

## Project Overview

The application is a minimal Node.js server built using the built-in `http` module. It is containerized using Docker and automatically tested, built, and deployed to a remote Linux server using GitHub Actions.

---

## Tech Stack

- Node.js
- Docker
- GitHub Actions
- DockerHub
- SSH-based Remote Deployment
- Linux Server (Cloud VM)

---

## Application Details

The app runs a basic HTTP server on port 3000 and returns:

Hello, Node.js!

### Run Locally

```bash
node app.js
```

Open in browser:

```
http://localhost:3000
```

---

## Docker Setup

### Build Docker Image

```bash
docker build -t newapp .
```

### Run Docker Container

```bash
docker run -d -p 3000:3000 newapp
```

Access:

```
http://localhost:3000
```

---

## CI/CD Pipeline Architecture

The GitHub Actions workflow consists of three main stages:

### 1. Testing Stage
- Starts the Node.js application
- Validates response using curl
- Fails pipeline if application is not reachable
- Ensures only working builds proceed

### 2. Build Stage
- Builds Docker image
- Tags image with:
  - latest
  - commit SHA
- Pushes images securely to DockerHub

### 3. Deployment Stage
- Connects to remote server via SSH
- Pulls latest Docker image
- Stops and removes old container
- Starts new container
- Performs post-deployment health check
- Cleans up unused Docker images

---

## Required GitHub Secrets

Add the following secrets under:

Repository → Settings → Secrets and variables → Actions

- DOCKER_USERNAME (docker hub username)
- DOCKER_PASSWORD (docker hub credentials)
- SERVER_HOST (VM public IP Address)
- SERVER_USER (VM Server Username)
- SERVER_SSH_KEY (SSH credentials)

---

## Deployment Flow

1. Code is pushed to the main branch
2. GitHub Actions triggers automatically
3. Application is tested
4. Docker image is built and pushed to DockerHub
5. Server pulls latest image
6. Old container is replaced
7. Health check validates deployment

---

## Production-Oriented Practices Implemented

- Fail-fast error handling
- Automated validation before deployment
- Commit-based image tagging
- Secure secret management
- Clean container lifecycle management
- Post-deployment verification
- Automated Docker image cleanup

---

---

This project demonstrates a production mindset applied even to a simple Node.js HTTP service, showcasing practical DevOps automation and container deployment strategies.
