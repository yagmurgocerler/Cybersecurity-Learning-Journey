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


# 2. Running Your First Container

## Overview

Docker containers are created and started using the `docker run` command. A container is launched from an existing Docker image and executes the commands defined inside that image or commands provided by the user.

---

## Docker Run Syntax

General syntax:

```bash
docker run [OPTIONS] IMAGE_NAME [COMMAND] [ARGUMENTS...]
```

- **OPTIONS** → Configure how the container runs.
- **IMAGE_NAME** → The Docker image to use.
- **COMMAND** → Command to execute inside the container.
- **ARGUMENTS** → Optional parameters for the command.

---

## Running a Container Interactively

To start a container and open a shell inside it:

```bash
docker run -it helloworld /bin/bash
```

### Explanation

- `docker run` → Creates and starts a new container.
- `-i` → Keeps standard input open (interactive mode).
- `-t` → Allocates a terminal session.
- `helloworld` → Docker image.
- `/bin/bash` → Starts a Bash shell inside the container.

After launching successfully, the prompt changes:

```bash
root@30eff5ed7492:/#
```

The hostname displayed is the container ID.

---

## Common Docker Run Options

| Option | Description | Example |
|---------|-------------|---------|
| `-d` | Run the container in the background (detached mode). | `docker run -d nginx` |
| `-it` | Interactive terminal session. | `docker run -it ubuntu /bin/bash` |
| `-v` | Mount a host directory or file into the container. | `docker run -v /host/data:/container/data ubuntu` |
| `-p` | Map host ports to container ports. | `docker run -p 80:80 nginx` |
| `--rm` | Automatically remove the container after it exits. | `docker run --rm ubuntu` |
| `--name` | Assign a custom name to the container. | `docker run --name webserver nginx` |

---

## Listing Running Containers

Display currently running containers:

```bash
docker ps
```

Example output:

```bash
CONTAINER ID   IMAGE        COMMAND   STATUS     PORTS              NAMES
a913a8f6e30f   helloworld   sleep     Up 3 days  0.0.0.0:8000->8000 helloworld
```

Information displayed includes:

- Container ID
- Image
- Running command
- Creation time
- Current status
- Port mappings
- Container name

---

## Listing All Containers

To display both running and stopped containers:

```bash
docker ps -a
```

This is useful for viewing exited containers and troubleshooting previous sessions.

---

## Key Takeaways

- `docker run` starts a container from an image.
- Interactive containers use the `-it` option.
- Common options like `-d`, `-p`, `-v`, `--rm`, and `--name` customize container behavior.
- `docker ps` lists active containers.
- `docker ps -a` lists all containers, including stopped ones.


# 3. Building Your First Container

## Overview

In this task, I learned how Dockerfiles define the instructions for building Docker images. I also learned the essential Dockerfile instructions, how to build an image using `docker build`, and best practices for writing efficient Dockerfiles.

---

# What is a Dockerfile?

A **Dockerfile** is a text file containing instructions that Docker follows to build an image.

General syntax:

```dockerfile
INSTRUCTION argument
```

Each instruction performs a specific action during the image build process.

---

# Essential Dockerfile Instructions

| Instruction | Description | Example |
|------------|-------------|---------|
| `FROM` | Specifies the base image. Every Dockerfile must begin with this instruction. | `FROM ubuntu:22.04` |
| `RUN` | Executes commands while building the image. | `RUN whoami` |
| `COPY` | Copies files from the host into the container. | `COPY ./app /app` |
| `WORKDIR` | Sets the working directory inside the container. | `WORKDIR /` |
| `CMD` | Defines the default command executed when the container starts. | `CMD ["/bin/bash"]` |
| `EXPOSE` | Documents which port the container will use. | `EXPOSE 80` |

---

# Example Dockerfile

The following Dockerfile:

- Uses Ubuntu 22.04 as the base image.
- Sets the working directory.
- Creates a file named `helloworld.txt`.

```dockerfile
FROM ubuntu:22.04

WORKDIR /

RUN touch helloworld.txt
```

> **Note:** The available commands in the `RUN` instruction depend on the operating system specified in the `FROM` instruction.

---

# Building a Docker Image

Docker images are built using:

```bash
docker build -t <image-name> .
```

Example:

```bash
docker build -t helloworld .
```

Explanation:

- `docker build` → Builds a Docker image.
- `-t` → Assigns a name (tag) to the image.
- `helloworld` → Image name.
- `.` → Uses the current directory as the build context.

---

# Verifying the Build

List all local images:

```bash
docker image ls
```

Example output:

```text
REPOSITORY   TAG       IMAGE ID       SIZE
helloworld   latest    4b11fc80fdd5   77.8MB
ubuntu       22.04     2dc39ba059dc   77.8MB
```

Notice that both images appear because the custom image is built on top of the Ubuntu base image.

---

# Building a Web Server Image

A Dockerfile can also install applications.

Example:

```dockerfile
FROM ubuntu:22.04

RUN apt-get update -y
RUN apt-get install apache2 -y

EXPOSE 80

CMD ["apache2ctl", "-D", "FOREGROUND"]
```

This Dockerfile:

- Uses Ubuntu 22.04.
- Installs Apache2.
- Exposes port 80.
- Starts the Apache web server when the container launches.

Build the image:

```bash
docker build -t webserver .
```

Run the container:

```bash
docker run -d --name webserver -p 80:80 webserver
```

---

# Optimizing Dockerfiles

Efficient Dockerfiles are easier to maintain and build faster.

### Best Practices

- Install only the required packages.
- Remove unnecessary cached files.
- Use lightweight base images whenever possible.
- Reduce the number of image layers.

---

# Reducing Layers

Instead of writing:

```dockerfile
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install apache2 -y
RUN apt-get install net-tools -y
```

Combine commands into a single layer:

```dockerfile
RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install apache2 -y && \
    apt-get install net-tools -y
```

Using fewer layers improves build performance and reduces image size.

---

# Key Takeaways

- Dockerfiles define how Docker images are built.
- Every Dockerfile starts with a `FROM` instruction.
- `RUN`, `COPY`, `WORKDIR`, `CMD`, and `EXPOSE` are fundamental Dockerfile instructions.
- Images are built using `docker build`.
- `docker image ls` verifies successful image creation.
- Well-optimized Dockerfiles build faster and produce smaller images.



# 4. Docker Compose

## Overview

In this task, I learned how Docker Compose simplifies the management of multi-container applications. Instead of creating and connecting containers individually, Docker Compose allows multiple services to be defined and managed using a single configuration file.

---

# What is Docker Compose?

Docker Compose is a tool for defining and running multi-container Docker applications.

Instead of starting each container manually, Docker Compose allows all related containers to be managed together.

### Benefits

- Start multiple containers with a single command.
- Automatically create networks between containers.
- Easy to share project configurations.
- Simplifies maintenance and scaling.

---

# Common Docker Compose Commands

| Command | Description | Example |
|---------|-------------|---------|
| `docker-compose up` | Build (if necessary) and start all services. | `docker-compose up` |
| `docker-compose start` | Start existing containers. | `docker-compose start` |
| `docker-compose stop` | Stop running containers without removing them. | `docker-compose stop` |
| `docker-compose down` | Stop and remove containers, networks, and related resources. | `docker-compose down` |
| `docker-compose build` | Build images without starting containers. | `docker-compose build` |

---

# Why Use Docker Compose?

Consider an e-commerce application consisting of:

- Apache web server
- MySQL database

Without Docker Compose, both containers must be created manually:

```bash
docker network create ecommerce

docker run -p 80:80 --name webserver --net ecommerce webserver

docker run --name database --net ecommerce mysql
```

Managing multiple containers manually quickly becomes difficult as projects grow.

Using Docker Compose, all services can be started with a single command:

```bash
docker-compose up
```

Docker Compose automatically:

- Creates the required network
- Starts all defined services
- Connects containers together

---

# Docker Compose File

Docker Compose uses a configuration file named:

```text
docker-compose.yml
```

This file defines all services, networks, volumes, and other configuration options.

> **Note:** YAML files are indentation-sensitive. Consistent indentation (commonly two spaces) is required.

---

# Common Docker Compose Instructions

| Instruction | Description | Example |
|------------|-------------|---------|
| `version` | Specifies the Compose file version. | `version: '3.3'` |
| `services` | Defines all application services. | `services:` |
| `build` | Path to the Dockerfile used to build the image. | `build: ./web` |
| `image` | Uses an existing Docker image. | `image: mysql:latest` |
| `ports` | Maps host ports to container ports. | `80:80` |
| `volumes` | Mounts host directories into containers. | `./data:/var/lib/mysql` |
| `environment` | Defines environment variables. | `MYSQL_ROOT_PASSWORD=password` |
| `networks` | Specifies the network(s) a service belongs to. | `ecommerce` |

---

# Example docker-compose.yml

```yaml
version: '3.3'

services:
  web:
    build: ./web
    ports:
      - "80:80"
    networks:
      - ecommerce

  database:
    image: mysql:latest
    environment:
      - MYSQL_DATABASE=ecommerce
      - MYSQL_USERNAME=root
      - MYSQL_ROOT_PASSWORD=helloworld
    networks:
      - ecommerce

networks:
  ecommerce:
```

This configuration:

- Builds the web service from a Dockerfile.
- Uses the official MySQL image.
- Connects both services to the same network.
- Publishes port **80** for the web server.

---

# Project Structure

Example directory layout:

```text
project/
│
├── docker-compose.yml
└── web/
    └── Dockerfile
```

---

# Key Takeaways

- Docker Compose manages multiple containers as a single application.
- Services are defined in a `docker-compose.yml` file.
- `docker-compose up` starts all services with one command.
- Containers can automatically communicate through shared networks.
- Docker Compose improves portability, scalability, and project maintenance.


# 5. Docker Architecture

## Overview

In this task, I learned how Docker works internally using a client-server architecture. Docker consists of two main components that communicate with each other through a socket, allowing containers to be managed efficiently.

---

# Docker Components

When Docker is installed, two main programs are installed:

- Docker Client
- Docker Server (Docker Daemon)

Docker follows a **client-server model**, where the client sends requests and the server processes them.

---

# Docker Client

The Docker Client is the command-line interface (CLI) used to interact with Docker.

Example:

```bash
docker run helloworld
```

When this command is executed, the Docker Client sends a request to the Docker Server to create and start a container using the **helloworld** image.

---

# Docker Server

The Docker Server (Docker Daemon) receives requests from the Docker Client and performs actions such as:

- Building images
- Running containers
- Stopping containers
- Removing containers
- Managing Docker resources

The Docker Server exposes an API that the Docker Client communicates with.

---

# Docker Socket

Communication between the Docker Client and Docker Server happens through a **Docker socket**.

A socket is an operating system feature that enables **Interprocess Communication (IPC)**, allowing different processes to exchange data.

In Docker:

```text
Docker Client
      │
      ▼
 Docker Socket
      │
      ▼
Docker Server
```

The Docker Client sends commands through the socket, and the Docker Server processes them.

---

# Docker API

The Docker Server exposes an API that listens for requests.

Although the Docker Client is the most common way to interact with Docker, other tools can also communicate with the Docker API, such as:

- `curl`
- Postman
- Custom applications

These tools can send API requests directly to the Docker Server.

---

# Remote Docker Access

The Docker Server can be configured to accept requests from remote machines.

This allows administrators to manage Docker remotely.

However, exposing the Docker API without proper security is dangerous because an attacker could:

- Start containers
- Stop containers
- Delete containers
- Access running services

For this reason, remote Docker access should always be secured.

---

# Key Takeaways

- Docker uses a **client-server architecture**.
- The Docker Client sends commands to the Docker Server.
- The Docker Server manages Docker images and containers.
- Communication happens through the **Docker socket**.
- The Docker Server exposes an API that can also be accessed using tools like `curl` or Postman.
- Remote Docker management is powerful but must be configured securely.
