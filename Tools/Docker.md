# Docker

## Tutorials

- https://docker-curriculum.com/
- https://www.docker.com/play-with-docker/
- https://www.docker.com/101-tutorial/
- https://docs.docker.com/get-started/
- https://www.hostinger.com/tutorials/docker-tutorial/
- https://www.geeksforgeeks.org/devops/docker-tutorial/
- https://learncloudnative.com/blog/2020-04-29-beginners-guide-to-docker
- https://medium.com/@nomannayeem/the-one-docker-tutorial-every-beginner-developer-actually-needs-f94a5774da27

## Commands

### https://docker-curriculum.com/

```
docker run hello-world

docker pull busybox
docker images
docker run busybox
docker run busybox echo "hello from busybox"
docker ps  # show all containers that are running
docker ps -a  # show list of containers that we ran

docker run -it busybox sh  # attach to an interative tty in the container

docker run --help
```

`docker run` may be the command you will use the most.

