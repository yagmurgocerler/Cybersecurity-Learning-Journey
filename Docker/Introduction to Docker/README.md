# Introduction to Docker

## Overview

In this room, I learned the fundamentals of Docker, including Docker images, image management, and the basic syntax used to interact with Docker. These concepts provide the foundation for creating and managing containers.

# 1. Managing Docker Images

Docker containers require images before they can run. Images contain the instructions that define what a container will execute.

## Downloading an Image

Docker images can be downloaded using:

```bash
docker pull <image>
```

Example:

```bash
docker pull nginx
```

Docker downloads the latest version of the **nginx** image.

Example output:

```text
Using default tag: latest
latest: Pulling from library/nginx
Status: Downloaded newer image for nginx:latest
```

---

## Image Tags

Images use **tags** to identify different versions.

Examples:

| Command | Description |
|----------|-------------|
| `docker pull ubuntu` | Downloads the latest version |
| `docker pull ubuntu:latest` | Same as above |
| `docker pull ubuntu:22.04` | Downloads Ubuntu 22.04 |
| `docker pull ubuntu:20.04` | Downloads Ubuntu 20.04 |
| `docker pull ubuntu:18.04` | Downloads Ubuntu 18.04 |

> **Note:** Docker assumes the `latest` tag if no tag is specified.

---

## Listing Images

To display all downloaded images:

```bash
docker image ls
```

Example:

```text
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       22.04     2dc39ba059dc   10 days ago   77.8MB
nginx        latest    2b7d6430f78d   2 weeks ago   142MB
```

Explanation of each column:

| Column | Description |
|---------|-------------|
| Repository | Image name |
| Tag | Image version |
| Image ID | Unique image identifier |
| Created | Creation time |
| Size | Image size |

---

## Removing an Image

Images can be removed using:

```bash
docker image rm <image>:<tag>
```

Example:

```bash
docker image rm ubuntu:22.04
```

Example output:

```text
Untagged: ubuntu:22.04
Deleted: sha256:...
```

To verify the image has been removed:

```bash
docker image ls
```

The deleted image will no longer appear in the list.

---

# Commands Summary

| Command | Purpose |
|----------|---------|
| `docker pull nginx` | Download an image |
| `docker pull ubuntu:22.04` | Download a specific version |
| `docker image ls` | List downloaded images |
| `docker image rm ubuntu:22.04` | Remove an image |

---

# Key Takeaways

- Docker containers run from images.
- Images are downloaded using `docker pull`.
- Tags specify image versions.
- `docker image ls` lists local images.
- `docker image rm` removes images.
- The `latest` tag is used by default if no tag is specified.
