# 🐳 Docker Basic Commands Cheat Sheet

This document covers the most commonly used Docker commands for beginners. Use it for **quick reference, practice, and interview revision**.

---

## 🔍 Check Docker Version

```bash
docker --version
```

---

## 📦 Pull an Image

Downloads an image from Docker Hub.

```bash
docker pull python:3.10
```

---

## ▶️ Run a Container

Runs a container from an image.

```bash
docker run python:3.10
```

---

## 🧑‍💻 Run Container in Interactive Mode

Useful for debugging or exploring a container.

```bash
docker run -it ubuntu bash
```

* `-i` → Interactive
* `-t` → Allocate terminal

---

## 🌐 Port Mapping (Very Common)

Maps a container port to the host machine.

```bash
docker run -p 8080:80 nginx
```

* Host port `8080` → Container port `80`

---

## 💾 Volumes (Data Persistence)

Mounts a local directory into the container.

```bash
docker run -v $(pwd):/app python:3.10
```

* Keeps data even if the container is removed

---

## 🕶️ Run Container in Detached Mode

Runs the container in the background.

```bash
docker run -d busybox
```

---

## 📋 List Containers

### Running containers

```bash
docker ps
```

### All containers (running + stopped)

```bash
docker ps -a
```

---

## 🖼️ List Docker Images

```bash
docker images
```

---

## ⏹️ Stop a Container

```bash
docker stop <container_id>
```

---

## 🗑️ Remove a Container

```bash
docker rm <container_id>
```

---

## 🧹 Remove an Image

```bash
docker rmi <image_id>
```

---
## ▶️ Run a Container

Runs a container from an image.

```bash
docker run <image>
```

---
## 🛑 Run Container in Detached Mode

Runs a container in the background.

```bash
docker run -d <image>
```

* `-d` → Detached (background)

---
## 🏷️ Run Container with a Name

Assigns a custom name to the container.

```bash
docker run --name my-container <image>
```

---
## 🌐 Run Container with Port Mapping

Maps a container port to the host machine.

```bash
docker run -p 8080:80 <image>
```

* `8080` → Host port  
* `80` → Container port

---
## 📂 Run Container with Volume Mount

Mounts a host directory into the container.

```bash
docker run -v $(pwd):/app <image>
```

* `$(pwd)` → Current host directory  
* `/app` → Container directory

---
## 🧑‍💻 Run Container in Interactive Mode

Useful for debugging or exploring a container.

```bash
docker run -it <image> sh
```

* `-i` → Interactive  
* `-t` → Allocate terminal  

---
## 📋 List Running Containers

Shows only running containers.

```bash
docker ps
```

---
## 📋 List All Containers

Shows running and stopped containers.

```bash
docker ps -a
```

---
## 📜 View Container Logs

Displays logs of a container.

```bash
docker logs <container>
```

---
## 🔌 Attach to a Running Container

Connects your terminal to a running container.

```bash
docker attach <container>
```

---
## ⏹️ Stop a Container

Gracefully stops a running container.

```bash
docker stop <container>
```

---
## 💀 Kill a Container

Force stops a container immediately.

```bash
docker kill <container>
```

---
## 🧹 Stop All Running Containers

Stops every running container at once.

```bash
docker stop $(docker ps -q)
```

* `docker ps -q` → Returns container IDs only

---
## ▶️ Start a Stopped Container

Starts an existing stopped container.

```bash
docker start <container>
```

---
## 🗑️ Remove a Container

Deletes a stopped container.

```bash
docker rm <container>
```

---
## 🗑️ Force Remove a Running Container

Stops and removes a container in one command.

```bash
docker rm -f <container>
```

* `-f` → Force remove

---
## 🧹 Remove All Stopped Containers

Cleans up unused containers.

```bash
docker container prune
```

---
## 📤 Copy File from Container to Host

Copies files from container to local system.

```bash
docker cp <container>:/path/to/file ./
```




**Tip:** Practice these commands daily to build confidence with Docker.
