# Docker curriculum

https://docker-curriculum.com/

## Commands

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

<br/>

## Webapps with Docker

### Static Sites

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


### Docker Images

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

### Dockerfile

A Dockerfile is a simple text file that contains a list of commands that the Docker client calls while creating an image. 

Dockerfile:

```
FROM python:3.8

# set a directory for the app
WORKDIR /usr/src/app

# copy all the files to the container
COPY . .

# install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# define the port number the container should expose
EXPOSE 5000

# run the command
CMD ["python", "./app.py"]
```

Build the Docker image:
```
docker build -t yourusername/catnip .
docker run -p 8888:5000 yourusername/catnip
```

See the app running at: http://localhost:8888

<br/>

## Multi-container environments

```
docker search elasticsearch
docker pull docker.elastic.co/elasticsearch/elasticsearch:6.3.2
docker run -d --name es -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.3.2

docker container ls  # same as: docker ps
docker container logs es

curl 0.0.0.0:9200
```

Dockerfile for the flask app:

```
# start from base
FROM ubuntu:24.04

LABEL maintainer=""

# install system-wide deps for python and node
RUN apt-get -yqq update
RUN apt-get -yqq install python3.12 python3.12-dev python3.12-venv curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_20.x | bash
RUN apt-get install -yq nodejs

# Create Python virtual environment
RUN python3.12 -m venv /opt/venv

# Make virtual environment the default Python environment
ENV PATH="/opt/venv/bin:$PATH"


# copy our application code
ADD flask-app /opt/flask-app
WORKDIR /opt/flask-app

# fetch app specific deps
RUN npm install
RUN npm run build
RUN pip3 install -r requirements.txt

# expose port
EXPOSE 5000

# start app
CMD [ "python3", "./app.py" ]
```

- The yqq flag is used to suppress output and assumes "Yes" to all prompts.
- The ADD command copies our application into a new volume in the container - /opt/flask-app
- We also set this as our working directory, so that the following commands will be run here

```
docker build -t yourusername/foodtrucks-web .
docker run -P --rm yourusername/foodtrucks-web
```


When docker is installed, it creates three networks automatically.
```
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
c2c695315b3a        bridge              bridge              local
a875bec5d6fd        host                host                local
ead0e804a67b        none                null                local
```

The bridge network is the network in which containers are run by default. 
So that means that when I ran the ES container, it was running in this bridge network.

Let's find out by running our flask container and trying to access this IP.
We see that we can indeed talk to ES on 172.17.0.2:9200.

```
% docker run -it --rm txchen2017/foodtrucks-web bash
root@3ae7ff968fbd:/opt/flask-app# 
root@3ae7ff968fbd:/opt/flask-app# curl 172.17.0.2:9200
{
  "name" : "R6kFrS9",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "TBT3WLm8TdaV-AqPyc3J6A",
  "version" : {
    "number" : "6.3.2",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "053779d",
    "build_date" : "2018-07-20T05:20:23.451332Z",
    "build_snapshot" : false,
    "lucene_version" : "7.3.1",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}
root@3ae7ff968fbd:/opt/flask-app# exit
```

2 questions:
- How do we tell the Flask container that es hostname stands for 172.17.0.2 or some other IP since the IP can change?
- Since the bridge network is shared by every container by default, this method is not secure. How do we isolate our network?

Docker allows us to define our own networks while keeping them isolated using the `docker network` command.

```
% docker network create foodtrucks-net
04d95065828395d23dd26402a2c6ef11ddef524a9fb1aad40a5112c5b31d3a91
% docker network ls
NETWORK ID     NAME             DRIVER    SCOPE
faa272ab71a0   bridge           bridge    local
04d950658283   foodtrucks-net   bridge    local
83f17a299dda   host             host      local
3ffde8132057   kind             bridge    local
91064ce4bd45   none             null      local
```
