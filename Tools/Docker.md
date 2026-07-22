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

```
docker rm ${docker_id1 docker_id2 ...}

docker rm $(docker ps -a -q -f status=exited)  # remove all exited dockers
# -q flag, only returns the numeric IDs and -f filters output based on conditions provided

# the --rm flag that can be passed to docker run which automatically deletes the container
# once it's exited from. For one off docker runs, --rm flag is very useful.

docker container prune  # remove all stopped containers
```

Lastly, you can also delete images that you no longer need by running `docker rmi`.

### Terminology that is used frequently in the Docker ecosystem.

- Images - The blueprints of our application which form the basis of containers. In the demo above, we used the docker pull command to download the busybox image.
- Containers - Created from Docker images and run the actual application. We create a container using docker run which we did using the busybox image that we downloaded. A list of running containers can be seen using the docker ps command.
- Docker Daemon - The background service running on the host that manages building, running and distributing Docker containers. The daemon is the process that runs in the operating system which clients talk to.
- Docker Client - The command line tool that allows the user to interact with the daemon. More generally, there can be other forms of clients too - such as Kitematic which provide a GUI to the users.
- Docker Hub - A registry of Docker images. You can think of the registry as a directory of all available Docker images. If required, one can host their own Docker registries and can use them for pulling images.

