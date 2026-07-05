# Docker Notes (Beginner Friendly)

## Docker Image Layers

A Docker Image is made up of multiple **read-only layers**.

When we create a container from an image, Docker adds one extra layer on top called the **Container Layer**.

This layer is **writable**, meaning any files you create or modify inside the container are stored here.

```text
+-----------------------------+
| Container Layer (Writable)  |
+-----------------------------+
| Layer 3 (Read Only)         |
+-----------------------------+
| Layer 2 (Read Only)         |
+-----------------------------+
| Base Layer (Linux OS, etc.) |
+-----------------------------+
```

### Key Points

- Image layers are **read-only**.
- Container layer is **writable**.
- Deleting the container also removes everything stored in the container layer.

---

# Docker Images

A Docker Image is simply a collection of multiple layers.

Docker downloads only the layers that are missing.

If some layers already exist on your computer, Docker reuses them instead of downloading them again.

This saves:

- Download time
- Internet bandwidth
- Disk space

Example:

```text
Image A

Layer 3
Layer 2
Base Layer
```

If another image also uses the same Base Layer and Layer 2, Docker downloads only the new layer.

---

# Port Binding

Every Docker container has its own private network.

This means two different containers can both use the same internal port without any problem.

Example:

```text
Container A
3306

Container B
3306
```

Both containers are isolated, so there is no conflict.

---

## Accessing a Container from Your Computer

To access a container from your host machine, we use **Port Binding**.

Command:

```bash
docker run -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
```

Example:

```bash
docker run -p 8080:3306 mysql
```

Here,

- **8080** → Host Machine Port
- **3306** → Container Port

This means:

```text
Host (8080)
      │
      ▼
Container (3306)
```

Now you can access the application through port **8080** on your computer.

---

## Can Two Containers Use the Same Host Port?

❌ No.

Example:

```bash
docker run -p 8080:3306 mysql
docker run -p 8080:3306 mysql
```

The second command will fail because **8080** is already being used.

Instead, use different host ports.

Example:

```bash
docker run -p 8080:3306 mysql
docker run -p 8081:3306 mysql
```

Now,

```text
Host 8080 ─────► Container A (3306)

Host 8081 ─────► Container B (3306)
```

Both containers still use port **3306**, but the host machine uses different ports.

---

# Summary

- Docker Images are made of multiple **read-only layers**.
- A container adds one **writable layer** on top of the image.
- Docker reuses existing layers to save download time and storage.
- Every container has its own private network.
- Containers can use the same internal port.
- Host ports must be unique.
- Port binding connects a **Host Port** to a **Container Port**.