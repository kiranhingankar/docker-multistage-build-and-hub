# Docker Multi-Stage Builds 🚀

This repository demonstrates how to optimize Docker images using **Multi-Stage Builds** and follow Docker image best practices.

---

# 📌 Project Objective

Learn how to:

- Build Docker images using single-stage and multi-stage Dockerfiles
- Reduce Docker image size
- Push Docker images to Docker Hub
- Apply production-ready Docker best practices

---

# 📁 Project Structure

```text
.
├── app.js
├── package.json
├── Dockerfile.single
├── Dockerfile.multi
├── Dockerfile.optimized
└── README.md
```

---

# 🟢 Simple Node.js Application

## app.js

```js
console.log("Hello from Docker Multi-Stage Build!");
```

---

# 🐳 Single-Stage Docker Build

## Dockerfile.single

```dockerfile
FROM node:22

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

CMD ["node", "app.js"]
```

---

## Build Single-Stage Image

```bash
docker build -f Dockerfile.single -t node-build-single:v1 .
```

## Check Image Size

```bash
docker images
```

Example:

| IMAGE | SIZE |
|------|------|
| node-build-single:v1 | 409MB |

---

# 🚀 Multi-Stage Docker Build

## Dockerfile.multi

```dockerfile
# Stage 1 - Builder
FROM node:22 AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Stage 2 - Production
FROM node:22-alpine

WORKDIR /app

COPY --from=builder /app .

CMD ["node", "app.js"]
```

---

## Build Multi-Stage Image

```bash
docker build -f Dockerfile.multi -t node-build-multi:v1 .
```

## Check Optimized Image Size

```bash
docker images
```

Example:

| IMAGE | SIZE |
|------|------|
| node-build-multi:v1 | 57.1MB |

---

# 📊 Size Comparison

| Build Type | Image Size |
|------|------|
| Single-Stage Build | 409MB |
| Multi-Stage Build | 57.1MB |

---

# 💡 Why Multi-Stage Builds?

Multi-stage builds help:

- Remove unnecessary build dependencies
- Reduce final image size
- Improve security
- Speed up deployments
- Create production-ready containers

---

# 🔐 Docker Best Practices Used

✅ Multi-stage builds  
✅ Alpine base image  
✅ Non-root user  
✅ Minimal runtime image  
✅ Specific image tags  
✅ Reduced image layers  

---

# 🛠 Optimized Dockerfile

## Dockerfile.optimized

```dockerfile
# Build Stage
FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Production Stage
FROM node:22-alpine

WORKDIR /app

COPY --from=builder /app .

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

USER appuser

CMD ["node", "app.js"]
```

---

# 📌 Docker Commands Used

## Build Docker Image

```bash
docker build -t image-name .
```

Builds a Docker image from the current directory.

---

## Build Using Specific Dockerfile

```bash
docker build -f Dockerfile.multi -t node-build-multi:v1 .
```

Builds an image using a specific Dockerfile.

---

## View Docker Images

```bash
docker images
```

Displays all local Docker images and their sizes.

---

## Login to Docker Hub

```bash
docker login
```

Authenticates Docker CLI with Docker Hub.

---

## Tag Docker Image

```bash
docker tag node-build-multi:v1 username/node-build-multi:v1
```

Creates a Docker Hub compatible image tag.

---

## Push Docker Image

```bash
docker push username/node-build-multi:v1
```

Uploads the image to Docker Hub.

---

## Pull Docker Image

```bash
docker pull username/node-build-multi:v1
```

Downloads the image from Docker Hub.

---

# 🐳 Docker Hub Repository

Replace with your repository link:

```text
https://hub.docker.com/r/yourusername/node-build-multi
```

---

# 📚 Key Learnings

- Multi-stage builds dramatically reduce image size
- Alpine images are lightweight and efficient
- Non-root users improve container security
- Docker Hub simplifies image distribution
- Optimized images improve deployment speed

---

# 🏷️ Tags

`Docker` `DevOps` `DockerHub` `Containers` `NodeJS` `MultiStageBuilds`

---

# 🙌 Acknowledgement

Part of the **#90DaysOfDevOps** challenge by TrainWithShubham.

---
