## 📦 What is Docker?

Docker is an open-source platform that enables developers to build, deploy, run, update, and manage applications within lightweight, self-contained units called **containers**. These containers package an application and all its dependencies — including code, libraries, system tools, and runtime — ensuring consistent execution across different environments.

---

### 🔧 Why Use Docker?

- ✅ **Portability & Consistency** – Works uniformly across environments.
- 🔒 **Isolation** – Keeps apps and dependencies independent.
- ⚡ **Efficiency** – Lightweight and fast compared to traditional VMs.
- 🧩 **Microservices Architecture** – Perfect for building distributed systems.

> 💡 Docker runs on hypervisor-based virtual machines but is more lightweight and efficient.

---

## 🧱 Docker Architecture

Docker uses a **client-server architecture**:

- **Docker Client** communicates with the **Docker Daemon** using a REST API (via UNIX sockets or TCP).
- Docker Compose allows you to manage multi-container apps from a single file.

### Key Components

#### 🔹 Docker Daemon (`dockerd`)
Handles:
- Image building
- Container lifecycle
- Volumes & Networks
- Registry communication

#### 🔹 Docker Client (`docker`)
CLI used to:
- Build and run containers
- Communicate with one or more daemons

#### 🔹 Docker Desktop
A GUI + CLI tool for:
- Container development
- Docker Daemon management
- Compose, CLI, Registry, Volumes, Networks, etc.

---

## 📦 Docker Registries

Registries are where Docker stores and retrieves container images.

- **Public Registry**: [Docker Hub](https://hub.docker.com)
- **Private Registry**: Self-hosted or cloud-based (e.g., AWS ECR, GitHub Packages)

### Commands:
- `docker pull <image>` – Download an image
- `docker push <repo>:<tag>` – Upload an image
- `docker login` – Authenticate to a registry

---

## 🧩 Docker Objects

| Object      | Description |
|-------------|-------------|
| **Image**   | A read-only template used to create containers. Created using Dockerfiles. |
| **Container** | A runnable instance of an image. Stateless unless connected to a volume. |
| **Volume**  | Persistent storage across container lifecycles. |
| **Plugin**  | Extensions for volumes, networks, or logging. |

### 🖼️ Image

- Built using `Dockerfile`
- Instructions form **layers**, which optimize rebuilds
- Example:
  ```dockerfile
  FROM node:18
  WORKDIR /app
  COPY . .
  RUN npm install
  CMD ["npm", "start"]
  
### 📦 Container
Created from an image

Isolated by default

Stateless unless configured with volumes

Example:

bash
Copy
Edit
docker run -d -p 3000:3000 my-app

### 💾 Volume
Keeps data alive even after container is removed

Created during container run, not at image build time

### 🔌 Plugin
Used for extended functionality like:

External volumes (e.g., EBS, NFS)

Network routing

Log aggregation

---

### 🧩 Docker Compose

Compose lets you define multi-container apps in a single docker-compose.yml file.

#### 📄 Sample: Without Compose (Manual)

- docker run -d --name db -e MYSQL_ROOT_PASSWORD=pass mysql 
- docker run -d --name backend --link db my-backend 
- docker run -d --name frontend -p 3000:3000 my-frontend 

#### ✅ With Compose (Simple & Declarative)

docker-compose up

---

### 🏗️ Compose Structure

version: "3.9"

services:
  db:
    image: mongo

  backend:
    build: ./backend
    ports:
      - "8000:8000"
    depends_on:
      - db

  frontend:
    build: ./frontend
    ports:
      - "3000:80"
    depends_on:
      - backend

---

  
### 🛠️ Common Docker Compose Commands
Command	Purpose
- docker-compose up	Start all services 
- docker-compose up -d	Start in background
- docker-compose down	Stop and remove containers
- docker-compose build	Build images
- docker-compose ps	List running containers
- docker-compose logs	Show service logs
- docker-compose exec <svc>	Run command inside container

### 🔍 Common Docker CLI Commands
Command	Description
- docker pull <image>:<tag>	Download image from registry
- docker images	List all local images
- docker run <image>	Run container from image
- docker run -d -p 80:80 <image>	Detached mode + port mapping
- docker ps	List running containers
- docker ps -a	List all containers
- docker stop <container_id>	Stop a running container
- docker start <container_id>	Start a stopped container
- docker rm <container_id>	Remove container
- docker rmi <image>	Remove image
- docker logs <container_id>	Show logs from container
- docker exec -it <container_id> bash	Interactive shell inside container
- docker build -t <image_name> .	Build image from Dockerfile
- docker tag <image> <repo>:<tag>	Tag image for pushing
- docker push <repo>:<tag>	Push image to registry
- docker network ls	List Docker networks
- docker volume ls	List Docker volumes
