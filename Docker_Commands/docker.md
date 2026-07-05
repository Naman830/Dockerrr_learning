# 🐳 Docker Commands Cheat Sheet

This document contains the most commonly used Docker commands for managing Docker images and containers.

---

## 1. Pull a Docker Image

Downloads an image from Docker Hub to your local machine.

### Syntax

```bash
docker pull <image_name>
```

### Example

```bash
docker pull nginx
```

---

## 2. List Downloaded Images

Displays all Docker images available on your local system.

### Command

```bash
docker images
```

### Example Output

```text
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
nginx        latest    abc123xyz      2 weeks ago   192MB
```

---

## 3. Run a Container

Creates and starts a new container from an image.

### Syntax

```bash
docker run <image_name>
```

### Example

```bash
docker run nginx
```

> This starts the container using the default settings.

---

## 4. Run a Container in Interactive Mode

Starts a container and allows you to interact with it through the terminal.

### Syntax

```bash
docker run -it <image_name>
```

### Example

```bash
docker run -it ubuntu
```

### What `-it` Means

- `-i` → Keeps the terminal input open.
- `-t` → Allocates a terminal (TTY).

This is commonly used when working inside Linux containers.

---

## 5. Stop a Running Container

Stops a running container gracefully.

### Syntax

```bash
docker stop <container_name>
```

or

```bash
docker stop <container_id>
```

### Example

```bash
docker stop my-container
```

or

```bash
docker stop a1b2c3d4
```

---

## 6. Start an Existing Container

Starts a container that has already been created but is currently stopped.

### Syntax

```bash
docker start <container_name>
```

or

```bash
docker start <container_id>
```

### Example

```bash
docker start my-container
```

or

```bash
docker start a1b2c3d4
```

---

# 📌 Summary

| Command | Purpose |
|----------|---------|
| `docker pull <image>` | Download an image from Docker Hub |
| `docker images` | List all downloaded images |
| `docker run <image>` | Create and start a container |
| `docker run -it <image>` | Run a container in interactive terminal mode |
| `docker stop <container>` | Stop a running container |
| `docker start <container>` | Start a stopped container |