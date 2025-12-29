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



**Tip:** Practice these commands daily to build confidence with Docker.
