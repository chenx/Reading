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


## https://docker-curriculum.com/

### Commands

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

#### Terminology that is used frequently in the Docker ecosystem.

- Images - The blueprints of our application which form the basis of containers. In the demo above, we used the docker pull command to download the busybox image.
- Containers - Created from Docker images and run the actual application. We create a container using docker run which we did using the busybox image that we downloaded. A list of running containers can be seen using the docker ps command.
- Docker Daemon - The background service running on the host that manages building, running and distributing Docker containers. The daemon is the process that runs in the operating system which clients talk to.
- Docker Client - The command line tool that allows the user to interact with the daemon. More generally, there can be other forms of clients too - such as Kitematic which provide a GUI to the users.
- Docker Hub - A registry of Docker images. You can think of the registry as a directory of all available Docker images. If required, one can host their own Docker registries and can use them for pulling images.

<br/>

### Webapps with Docker

#### Static Sites

```
docker run --rm -it ${registry}/static-site
```

```
docker run -d -P --name static-site ${registry}/static-site
docker port static-site  # show the running ports
```

-d will detach our terminal, -P will publish all exposed ports to random ports and finally --name corresponds to a name we want to give.

You can open http://localhost:32769 in your browser.

You can also specify a custom port to which the client will forward connections to the container:
```
docker run -p 8888:80 ${registry}/static-site
```

To stop a detached container, run docker stop by giving the container ID, or use name:
```
docker stop static-site
```

To deploy this on a real server you would just need to install Docker, and run the above Docker command.


#### Docker Images

```
docker images  # show list of images that are available locally
docker rmi ${image_id(s)}  # removes image(s)
docker image prune -a      # remove all images completely idle (i.e., no containers are built from it)
```

An image is similar to a git repository. Images can be committed with changes and have multiple versions.

```
docker pull ubuntu:18.04
```

To get a new Docker image you can either get it from a registry (such as the Docker Hub) or create your own.

You can also search for images directly from the command line using `docker search`.

Base and Child images:
- Base images are images that have no parent image, usually images with an OS like ubuntu, busybox or debian.
- Child images are images that build on base images and add additional functionality.

Official and user images:
- Official images: e.g., python, ubuntu, busybox and hello-world
- User images: e.g., user/image-name

#### Dockerfile

A Dockerfile is a simple text file that contains a list of commands that the Docker client calls while creating an image. 

