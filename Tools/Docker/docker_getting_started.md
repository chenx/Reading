# Docker: Getting Started

https://www.docker.com/101-tutorial/

### Run App getting-started

```
# -d: detached, -p: matching docker app port 80 to local port 8088
docker run -d -p 8088:80 docker/getting-started
```

Download: http://localhost:8088/assets/app.zip

Dockerfile:
```
FROM node:22-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

```
docker build -t getting-started .

docker run -dp 3000:3000 getting-started
```

Visit: http://localhost:3000

### Make changes

Update src/static/js/app.js

Build again:
```
docker build -t getting-started .
```

Stop the previous container with the same name:
```
docker ps

# Swap out <the-container-id> with the ID from docker ps
docker stop <the-container-id>

docker rm <the-container-id>

docker run -dp 3000:3000 getting-started
```

### Share our app: upload to Docker Hub

Create repo `getting-started` in Docker Hub (https://hub.docker.com)

```
docker tag getting-started txchen2017/getting-started
docker push txchen2017/getting-started
```

Run on a different device:
```
docker run -dp 3000:3000 txchen2017/getting-started
```

### Persist our DB

```
docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"
# check data.txt in Docker desktop, or from console:
docker exec <container-id> cat /data.txt
```

By default, TODO app's data is at: /etc/todos/todo.db

```
docker volume create todo-db
docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
```

Check where the persisted volumn is:

```
% docker volume inspect todo-db
[
    {
        "CreatedAt": "2026-07-25T06:12:07Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": null,
        "Scope": "local"
    }
]
```

However:
```
% sudo ls /var/lib/docker/volumes/todo-db/     
ls: /var/lib/docker/volumes/todo-db/: No such file or directory
```

```
This is expected on Docker Desktop for Mac.

The key point is that your Docker daemon is not running directly on macOS. Docker Desktop runs
Docker Engine inside a lightweight Linux VM. Therefore:

/var/lib/docker/volumes/todo-db/_data

exists inside the Docker Desktop Linux VM, not directly in your macOS filesystem.

Your output:

Mountpoint: /var/lib/docker/volumes/todo-db/_data

is the mountpoint from the Docker daemon's perspective.
```

To see what's inside the volume, the easiest way is to mount it into a temporary container:
```
docker run --rm -it \
  -v todo-db:/data \
  alpine \
  ls -la /data
```
Or interactively:
```
docker run --rm -it \
  -v todo-db:/data \
  alpine \
  sh
```
Then:
```
ls -la /data
```

You currently have:
```
MacBook
   │
   │ docker run
   ▼
Docker Desktop
   │
   ▼
Linux VM
   │
   └── /var/lib/docker/volumes/todo-db/_data
           │
           ▼
       todo-db volume
           │
           ▼
       /etc/todos
       inside getting-started container
```


<br/>

### Using Bind Mounts

Starting a Dev-Mode Container

```
cd /path/to/getting-started/app

# $(pwd -P): expand softlink to physical link. softlink causes problem.
docker run -dp 3000:3000 \
    -w /app -v "$(pwd -P):/app" \
    node:22-alpine \
    sh -c "yarn install && yarn run dev"

```


<br/>

### Multi-container Apps

#### Starting MySQL

1. Create the network.
```
docker network create todo-app
```

2. Start a MySQL container and attach it to the network. 
```
docker run -d \
    --network todo-app --network-alias mysql \
    -v todo-mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=todos \
    mysql:8.0
```

3. To confirm we have the database up and running, connect to the database and verify it connects.
```
docker exec -it <mysql-container-id> mysql -p
```

#### Connecting to MySQL

Use the nicolaka/netshoot container, which ships with a lot of tools that are useful for troubleshooting or debugging networking issues.

1. Start a new container using the nicolaka/netshoot image. Make sure to connect it to the same network.
```
docker run -it --network todo-app nicolaka/netshoot
```

2. Inside the container, we're going to use the dig command, which is a useful DNS tool. We're going to look up the IP address for the hostname mysql.

```
dig mysql
```

```
; <<>> DiG 9.20.23 <<>> mysql
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41729
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;mysql.				IN	A

;; ANSWER SECTION:
mysql.			600	IN	A	172.20.0.2

;; Query time: 1 msec
;; SERVER: 127.0.0.11#53(127.0.0.11) (UDP)
;; WHEN: Sat Jul 25 07:11:41 UTC 2026
;; MSG SIZE  rcvd: 44
```

#### Running our App with MySQL

Let's start our dev-ready container!

1. We'll specify each of the environment variables above, as well as connect the container to our app network.
```
docker run -dp 3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:22-alpine \
  sh -c "yarn install && yarn run dev"
```

2.  we look at the logs for the container (docker logs <container-id>), we should see a message indicating it's using the mysql database.

3. Open the app in your browser and add a few items to your todo list.

4. Connect to the mysql database and prove that the items are being written to the database. Remember, the password is secret.

If you take a quick look at the Docker Dashboard, you'll see that we have two app containers running. But, there's no real indication that they are grouped together in a single app. We'll see how to make that better next.


<br/>

### Using Docker Compose

Docker Compose is a tool that was developed to help define and share multi-container applications. With Compose, we can create a YAML file to define the services and with a single command, can spin everything up or tear it all down. 

#### Creating our Compose File

1. Inside of the app folder, create a file named docker-compose.yml (next to the Dockerfile and package.json files).

2. In the compose file, we'll start off by defining a list of services (or containers) we want to run as part of our application.

#### Defining the App Service

To remember, this was the command we were using to define our app container.
```
docker run -dp 3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:22-alpine \
  sh -c "yarn install && yarn run dev"
```

This was the command we used to define the mysql container:
```
docker run -d \
  --network todo-app --network-alias mysql \
  -v todo-mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=todos \
  mysql:8.0
```

Our complete docker-compose.yml should look like this:
```
services:
  app:
    image: node:22-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:8.0
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

#### Running our Application Stack

1. Make sure no other copies of the app/db are running first (docker ps and docker rm -f <ids>).

2. Start up the application stack using the docker compose up command. We'll add the -d flag to run everything in the background.
```
docker compose up -d
```
When we run this, we should see output like this:
```
[+] up 4/4
 ✔ Network app_default        Created      0.1s
 ✔ Volume app_todo-mysql-data Created      0.0s
 ✔ Container app-app-1        Started      1.1s
 ✔ Container app-mysql-1      Started      0.9s
```

You'll notice that the volume was created as well as a network! By default, Docker Compose automatically creates a network specifically for the application stack (which is why we didn't define one in the compose file).

3. Let's look at the logs using the `docker compose logs -f` command.


#### Seeing our App Stack in Docker Dashboard

#### Tearing it All Down

```
docker compose down
```

<br/>

### Image Building Best Practices

#### Security Scanning

```
# Deprecated.
# docker scan getting-started

# Use this instead:
docker scout cves getting-started
```

#### Image Layering

Did you know that you can look at how an image is composed? 
Using the `docker image history` command, you can see the command that was used to create each layer within an image.

```
docker image history getting-started

docker image history --no-trunc getting-started
```

#### Layer Caching

Going back to the image history output, we see that each command in the Dockerfile becomes a new layer in the image. You might remember that when we made a change to the image, the yarn dependencies had to be reinstalled. Is there a way to fix this? It doesn't make much sense to ship around the same dependencies every time we build, right?

To fix this, we need to restructure our Dockerfile to help support the caching of the dependencies. For Node-based applications, those dependencies are defined in the package.json file. So what if we start by copying only that file in first, install the dependencies, and then copy in everything else? Then, we only recreate the yarn dependencies if there was a change to the package.json. 

Change:
```
FROM node:22-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

to:

1. Update the Dockerfile to copy in the package.json first, install dependencies, and then copy everything else in.
```
FROM node:22-alpine
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --production
COPY . .
CMD ["node", "src/index.js"]
```

2. Create a file named `.dockerignore` in the same folder as the Dockerfile with the following contents.
```
node_modules
```
.dockerignore files are an easy way to selectively copy only image relevant files. 

3. Build a new image using docker build.
```
docker build -t getting-started .
```

4. Now, make a change to the src/static/index.html file (like change the <title> to say "The Awesome Todo App").

5. Build the Docker image now using `docker build -t getting-started .` again. This time, your output should look a little different.

You should notice that the build was MUCH faster! You'll see that several steps are using previously cached layers. We're using the build cache. Pushing and pulling this image and updates to it will be much faster as well. Hooray!


#### Multi-Stage Builds

Multi-stage builds are an incredibly powerful tool which help us by using multiple stages to create an image. They offer several advantages including:

    Separate build-time dependencies from runtime dependencies
    Reduce overall image size by shipping only what your app needs to run

**Maven/Tomcat Example**

When building Java-based applications, a JDK is needed to compile the source code to Java bytecode. However, that JDK isn't needed in production. You might also be using tools such as Maven or Gradle to help build the app. Those also aren't needed in our final image. Multi-stage builds help.

```
FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn package

FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 
```

In this example, we use one stage (called build) to perform the actual Java build with Maven. In the second stage (starting at FROM tomcat), we copy in files from the build stage. The final image is only the last stage being created (which can be overridden using the --target flag).

**React Example**

When building React applications, we need a Node environment to compile the JS code (typically JSX), SASS stylesheets, and more into static HTML, JS, and CSS. Although if we aren't performing server-side rendering, we don't even need a Node environment for our production build. Why not ship the static resources in a static nginx container?

```
FROM node:22 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

Here, we are using a node:18 image to perform the build (maximizing layer caching) and then copying the output into an nginx container. 


