# Medium Tutorial on Docker

## Basics

### Dockerfiles: The Blueprint

Example Dockerfile:
```
FROM node:14
# Start with this base foundation

WORKDIR /app
# Create a dedicated space for our stuff

COPY package*.json ./
# First bring in the shopping list

RUN npm install
# Get all the furniture and appliances

COPY . .
# Now bring in everything else

CMD ["npm", "start"]
# When someone visits, greet them this way
```

The most common instructions you’ll see:

    FROM: The starting point, what existing image are we building on?
    WORKDIR: Where inside the container we'll put our stuff
    COPY/ADD: Bring files from our computer into the image
    RUN: Execute commands during the build process
    ENV: Set environment variables
    EXPOSE: Document what ports the container will use
    CMD/ENTRYPOINT: What to run when the container starts

### Images: The Snapshot

- immutable
- layered
- tagged

A common mistake I see developers make is trying to modify an image directly. 
You can’t. You have to change the Dockerfile and rebuild.
```
# Build an image from a Dockerfile in current directory
docker build -t myapp:1.0 .

# List your images
docker images

# The same image can have multiple tags
docker tag myapp:1.0 myapp:latest
```

### Containers: The Running Instance

- Runnable: They’re the actual executing environment
- Isolated: They have their own filesystem, network, and process tree
- Ephemeral: By default, when a container stops, any changes to its filesystem are lost
- Based on an image: Every container starts from an image

```
# Run a container from an image
docker run myapp:1.0

# List running containers
docker ps

# Stop a container
docker stop container_id
```

### Putting It All Together

Here’s how these three components flow together in a typical workflow:

    You write a Dockerfile describing how to build your application
    You run docker build to create an image from that Dockerfile
    You run docker run to create a container from that image
    Your application runs inside the container

<br/>

## Your First Docker Container: Hands-On Without the Headaches

## Beyond Hello World: Using Docker in Real Projects

### Managing Your Images Without Losing Your Mind

```
# Don't just use 'latest' - use semantic versioning
docker build -t myapp:1.0.0 .

# Also tag as latest if it's the current version
docker tag myapp:1.0.0 myapp:latest

# List images to see what you've got
docker images

# Clean up unused images (this saved me 15GB once!)
docker image prune

# For a more aggressive cleanup (BE CAREFUL)
docker system prune -a
```

### Docker Compose: The Tool I Can’t Live Without

The moment your app needs more than one service (like an API and a database), `Docker Compose` becomes your best friend.

```
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
    depends_on:
      - db
  
  db:
    image: postgres:13
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=mydb

volumes:
  postgres_data:
```

With this file, a single `docker-compose up` command starts both services, 
sets up the networking between them, and mounts the necessary volumes.

### Volumes: Because Data Should Outlive Containers

Volumes are Docker’s answer to persistent data. Think of them as USB drives you can plug into containers:

```
# Create a named volume
docker volume create my_data

# Run a container with the volume mounted
docker run -v my_data:/app/data myapp

# With Docker Compose, it's even cleaner
# (as shown in the previous example)
```

There are three types of mounts, and knowing when to use each took me a while to figure out:

    Volumes (like above): Managed by Docker, best for persistent data
    Bind mounts: Connect container paths to host paths, perfect for development
    tmpfs mounts: Stored in memory only, good for sensitive info

For local development, I almost always use bind mounts to sync my code directory with the container:

```
# My go-to development setup
docker run -v $(pwd):/app myapp
```

This way, changes I make locally immediately appear in the container without rebuilding.


### Docker in a Team: Being a Good Container Citizen

Some team practices that have saved us endless headaches:

    Document all environment variables in a .env.example file
    Use docker-compose.override.yml for local customizations
    Agree on a tagging strategy (we use git hash for deployments)
    Set resource limits in your compose files to avoid container monopolizing resources

Don’t commit secrets to your Dockerfile or docker-compose.yml.

### The Docker Learning Curve

Core concepts:

    The relationship between Dockerfiles, images, and containers
    Why containers differ fundamentally from virtual machines
    How to build and run your own containers
    The basics of managing Docker in real projects

<br/>

## Where to Go From Here

- Dockerize one of your existing projects. Start small — pick something simple that would benefit from containerization.
- Learn Docker Compose properly: multi-container applications.
- Explore container orchestration. E.g., Kubernetes build on these concepts for production deployments.
- Join a container community: Docker’s official forums, Stack Overflow, and Reddit’s r/docker are all great places to ask questions.


