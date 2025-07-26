# 🛒 Online Shop – Dockerized Setup (Hackathon Solution)

This project demonstrates how to containerize a Node.js frontend app using both **single-stage** and **multi-stage** Docker builds. It includes setup instructions for **Git/GitHub**, **Linux**, and **Docker** on an EC2 instance.

---

## 📂 Branch to Work On

> **Branch:** `hackathon_solution`
> Files: `Dockerfile`, `Dockerfile_multistage`

---

## 🐙 Git & GitHub Workflow

1. **Fork** the project to your GitHub account.
2. **Clone** it into your EC2 instance:

   ```bash
   git clone https://github.com/abeyvaz/online_shop.git
   cd online_shop
   ```
3. **Initialize Git** (if not already initialized):

   ```bash
   git init
   ```
4. **Check file status**:

   ```bash
   git status
   ```
5. **Track changes**:

   ```bash
   git add Dockerfile Dockerfile_multistage
   ```
6. **Commit changes**:

   ```bash
   git commit -m "Initial Dockerfile changes"
   ```
7. **Push to remote branch**:

   ```bash
   git branch  # (optional: to list current branches)
   git push origin hackathon_solution
   ```

---

## 🐧 Linux Essentials for Docker Setup

These commands are useful for managing files and Docker installation on a Linux-based EC2 instance:

| Task                             | Command                          |
| -------------------------------- | -------------------------------- |
| Install Docker                   | `sudo apt-get install docker.io` |
| Add current user to Docker group | `sudo usermod -aG docker $USER`  |
| Switch to Docker group           | `newgrp docker`                  |
| Navigate filesystem              | `cd`, `cd ..`                    |
| List files and permissions       | `ls`, `ls -l`                    |
| Create/edit Dockerfile           | `vim Dockerfile`                 |

---

## 🐳 Docker Essentials

| Task                                    | Command                      |
| --------------------------------------- | ---------------------------- |
| Show running containers                 | `docker ps`                  |
| Show all containers (including stopped) | `docker ps -a`               |
| List Docker images                      | `docker images`              |
| Stop a container                        | `docker stop <container_id>` |
| Clean up stopped containers/images      | `docker system prune`        |

---

## 🏗️ Dockerfile – Multi-stage Production Build

This optimized build uses `node:20-alpine` and serves the static app using `serve`. It's fast, lightweight, and production-ready.

```dockerfile
# Stage 1: Build the app
FROM node:20-alpine AS builder

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy source code and build the app
COPY . .
RUN npm run build

# Stage 2: Serve the built app with 'serve'
FROM node:20-alpine

WORKDIR /app

# Install static file server
RUN npm install -g serve

# Copy only the built output from builder
COPY --from=builder /app/dist ./dist

# Expose the app's port
EXPOSE 5173

# Start the static server
CMD ["serve", "-s", "dist", "-l", "5173"]
```

---

## ✅ Summary

* ✔️ Dockerized with **multi-stage builds** for minimal image size.
* ✔️ Integrated with **Git version control**.
* ✔️ Linux and Docker setup on EC2 covered.
* ✔️ Ready for **deployment** with production-grade practices.





    



    

    

