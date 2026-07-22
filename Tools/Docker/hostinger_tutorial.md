# Hostinger Docker Tutorial

## Core Docker concepts

### Docker Engine

- Server (dockerd)
- API
- Docker CLI

### Docker Hub

The default public Docker registry.

```
docker pull <name>:<tag>

docker pull ubuntu:latest
```

### Docker images

```
docker images

docker build -t your-image-name:latest .
```

### Docker containers

```
docker run -it ubuntu /bin/bash
```

### Dockerfiles

A Dockerfile is a plain text file that contains a sequence of step-by-step instructions for building a Docker image. 
It defines everything from the base operating system to the environment variables and application code.

The most common key instructions in a Dockerfile and their purpose:

    FROM. Specifies the base image for a new build stage.
    RUN. Executes commands during the image build process.
    COPY or ADD. Copies files from the build context into the image.
    CMD or ENTRYPOINT. Defines the command that runs when the container starts.
    ENV. Sets environment variables that will be available during the build and at runtime.
    WORKDIR. Sets the working directory for the subsequent RUN, CMD, ENTRYPOINT, COPY, and ADD instructions.

```
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

### Docker Compose

`Docker Compose` is a tool that simplifies the definition and management of `multi-container applications` 
using a single configuration file, typically named `docker-compose.yml`.

Within the configuration file, developers can define all the containers, networks, and volumes to build a 
complex application stack. Then, they can start and manage all the containers, otherwise called services 
in the context of Docker Compose, with a single command.

```
services:
  web:
    build: ./web  # Build the image from Dockerfile in the ./web directory
    ports:
      - "8000:8000"  # Map host port 8000 to container port 8000
    depends_on:
      - db     # Wait for the db service to be started
      - redis  # Wait for the redis service to be started

  db:
    image: postgres:15  # Use the official PostgreSQL 15 image
    environment:
      POSTGRES_USER: myuser       # Set database username
      POSTGRES_PASSWORD: mypassword  # Set database password
      POSTGRES_DB: mydb           # Set initial database name
    volumes:
      - db-data:/var/lib/postgresql/data  # Persist database data using a named volume

  redis:
    image: redis:alpine  # Use a lightweight Redis image for caching

volumes:
  db-data:  # Define a named volume to store database data
```

Start all the services:
```
docker compose up -d
```

<br/>

## How to install Docker

### Understanding basic Docker commands

```
docker ps -a. Lists all containers, including those that are stopped.
docker pull <name>:<tag>. Downloads an image from the registry to your local machine.
docker rmi <image>. Deletes a local image.
docker stop <container>. Gracefully stops a running container.
docker rm <container>. Deletes a container.
```

https://www.hostinger.com/tutorials/docker-cheat-sheet/

### How to manage Docker volumes

`Volumes` are the preferred and primary mechanism to maintain data persistence in Docker, 
ensuring that data remains accessible even after a container is removed.

Docker offers three main types of storage:

- Volumes. Persistent data of your containers in the Docker storage area, which is typically /var/lib/docker/volumes/ on the host system.
- Bind mounts. Map a file or directory from the host machine directly into the container.
- tmpfs mounts. Store data in the host’s memory, which is lost when the container stops.

Here are the steps to create and manage a volume for persistent data:


- 1. Create a named volume using the following command. For example, this will set up a volume called my-database-data:
```
docker volume create my-database-data
```
- 2. Start your database container using the -v flag to map the named volume to the container’s internal data directory. The command looks like this:
```
docker run -d \
  --name my-database \
  -e MYSQL_ROOT_PASSWORD=securepassword \
  -v my-database-data:/var/lib/mysql \
  mysql:latest
```
- 3. Inspect the volume’s details and location on the host by running:
```
docker volume inspect my-database-data
```
- 4. To remove unused volumes that aren’t attached to any container and free up disk space, use:
```
docker volume prune -a
```

Instead of commands, you can declare and mount a volume by writing the configuration inside Docker Compose’s YAML file. 

Example: the following YAML configuration covers the steps for creating a volume and mounting a container above:

```
services:

  my-database:

    image: mysql:latest

    container_name: my-database

    environment:
      MYSQL_ROOT_PASSWORD: securepassword

    volumes:
      - my-database-data:/var/lib/mysql

volumes:
  my-database-data:
```

### How to create a Docker network

By default, containers are connected to a `bridge network`. 

To set up communication for a multi-service application, you should create a user-defined bridge network.

By default, Docker connects a container to a special network called the `default bridge network`, 
which allows it to communicate with the host. However, this default bridge network isn’t suitable 
for multi-container setups, as it has limited functionality in allowing services to connect with one another.

For multi-service applications, the best practice is to create a user-defined bridge network that 
enables containers to communicate with each other using their service names.

You can connect a container with a user-defined bridge network by adding the networks directive to the service’s 
configuration within Docker Compose’s YAML file. Here’s an example:
```
services:

  my-database:

    image: mysql:latest

    container_name: my-database

    environment:
      MYSQL_ROOT_PASSWORD: securepassword

    volumes:
      - my-database-data:/var/lib/mysql

    networks:
      - my-app-network #create a network
```

Alternatively, you can create a user-defined bridge network using the following command, with my-app-network being its name:
```
docker network create my-app-network
```

Then, you can start your container using Docker CLI with the –name flag to define the service name and –network 
to specify which network it attaches to. Here’s an example:
```
docker run -d \
  --name my-database \
  --network my-app-network \
  -e MYSQL_ROOT_PASSWORD=securepassword \
  -v my-database-data:/var/lib/mysql \
  mysql:latest
```

If you want to run and connect to another container, simply repeat the command with updated information 
about the service. In the following example, we add an extra -p flag to publish the container’s internal 
port 80 to the host machine’s port 8080 for external access:

```
docker run -d \
  --name my-webapp \
  --network my-app-network \
  -p 8080:80 \
  my-web-app-image:latest
```

<br/>

## Troubleshooting common Docker issues

### Container exits immediately

### Image layer caching issues

The simplest solution for this issue is to force a complete rebuild and ignore the layer cache. 
Do it by adding the –no-cache option when initiating the build process, like this command:

```
docker build --no-cache -t my-app:latest .
```

When installing packages using a Dockerfile, also explicitly include a command that prevents the package manager from reusing old layers with outdated package lists. In Debian-based distributions, you can achieve this by combining apt-get update and apt-get install -y –no-install-recommend in the same RUN statement like so:
```
RUN apt-get update && apt-get install -y --no-install-recommends
```

### Registry authentication failure

```
docker login my-registry.example.com
```

```
docker tag my-local-image:latest my-registry.example.com/my-repo/my-local-image:latest
docker push my-registry.example.com/my-repo/my-local-image:latest
```

<br/>

## What are the next steps to master Docker?

You need to go beyond the basics of using a single container and simple commands. 

In addition to Docker Compose, learning advanced orchestration tools like 
`<a href="https://www.hostinger.com/tutorials/how-to-create-docker-swarm/">Docker Swarm</a>` or `Kubernetes` 
is crucial for managing and scaling multiple containers across a cluster of machines.

Also, deepen your knowledge of network drivers, such as the `Overlay Network Driver` used in 
Docker Swarm mode for connecting hosts across a cluster.

Finally, explore Docker <a href="https://www.hostinger.com/tutorials/docker-use-cases">use cases</a> 
to gain a deeper understanding of how to utilize this 
containerization tool for various tasks during development and deployment.
