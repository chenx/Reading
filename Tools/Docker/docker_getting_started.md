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
docker tag getting-started YOUR-USER-NAME/getting-started
docker push YOUR-USER-NAME/getting-started
```

