# Docker: Getting Started

```
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
```

