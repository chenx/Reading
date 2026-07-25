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
FROM node:18-alpine
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


