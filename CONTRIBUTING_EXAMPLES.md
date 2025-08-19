# CONTRIBUTING\_EXAMPLES.md

*HelloContainers — Docker & Kubernetes Examples*

This document provides **practical examples** for contributing to the **HelloContainers** repository. All examples follow the **10 contribution principles** and are designed to be:

* **Enterprise-grade**: Suitable for production and scalable deployments.
* **Future-proof**: Compatible with local machines, on-prem servers, or cloud VMs.
* **Reproducible and maintainable**.

---

## 1. Clarity Over Cleverness

**Example: Simple Docker Image**

```dockerfile
# Dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y curl
CMD ["curl", "--version"]
```

```bash
# Build and run
docker build -t hello-curl .
docker run hello-curl
```

*Explanation*: Clear, explicit instructions for building and running a container.

---

## 2. Explicit Is Better Than Implicit

**Example: Docker Compose for Multi-Container Apps**

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
  app:
    image: myapp:latest
    depends_on:
      - web
```

*Explanation*: Explicitly defines services, ports, and dependencies.

---

## 3. Safety First

**Example: `.dockerignore` to Reduce Build Context**

```text
.git
node_modules
*.log
```

*Explanation*: Excludes unnecessary files to improve build efficiency and security.

---

## 4. Document As You Go

**Example: Dockerfile with Inline Documentation**

```dockerfile
# Base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy application files
COPY . /app

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose port
EXPOSE 80

# Run app
CMD ["python", "app.py"]
```

---

## 5. Test With Purpose

**Example: Local Testing of Docker Image**

```bash
docker build -t test-image .
docker run test-image
docker logs <container_id>
```

*Explanation*: Ensures images work as expected before deployment.

---

## 6. Consistency Is Key

**Example: Naming Conventions**

```bash
docker build -t username/hello-app:v1 .
docker push username/hello-app:v1
```

*Explanation*: Consistent image tags simplify management across environments.

---

## 7. Future-Proofing

**Example: Multi-Stage Docker Builds**

```dockerfile
# Build stage
FROM node:14 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Production stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
```

*Explanation*: Keeps images small and secure by separating build and production stages.

---

## 8. Scalability Matters

**Example: Kubernetes Deployment**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-app
  template:
    metadata:
      labels:
        app: hello-app
    spec:
      containers:
      - name: hello-app
        image: hello-app:v1
        ports:
        - containerPort: 8080
```

*Explanation*: Scalable deployment with multiple replicas.

---

## 9. Reproducibility Always

**Example: Versioning Images**

```bash
docker build -t hello-app:v1 .
docker push hello-app:v1
```

*Explanation*: Ensures specific versions are deployable consistently.

---

## 10. Community-Centric

**Example: Clear Contribution Instructions**

```markdown
# Contributing to HelloContainers

1. Fork the repository.
2. Clone your fork locally.
3. Create a new branch.
4. Make your changes and commit.
5. Push to your fork.
6. Open a pull request.

Ensure contributions follow Docker/K8s best practices and this guideline.
```

---

## Bonus: Best Practices

1. **Data & Config Management**: Store config files in `/configs/`.
2. **Security**: Avoid storing secrets in images; use environment variables or Kubernetes Secrets.
3. **Scalable Pipelines**: Use Docker Compose or K8s manifests to handle multi-service apps efficiently.

---
