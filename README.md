# Docker Cheat Sheet

List of useful Docker commands.


### Show the Docker version:
`docker version`

### Show the Docker info:
`docker info`

### Pull an image from Docker Hub:
`docker pull <image>`
#### Examples:
```
docker pull alpine
docker pull node
```

### List all images stored locally:
`docker images`

### List all images layers stored locally:
`docker images -q`

### List all running containers:
`docker ps`

### List all containers:
`docker ps -a`

### List all containers id:
`docker ps -aq`

### Filter containers by status:
`docker ps -f status=<status>`
#### Examples:
```
docker ps -f status=created
docker ps -f status=exited
```

### Remove container and the images associated with it:
`docker rmi <image>`
#### Example:
`docker rmi hello-world`

### Remove just the container:
`docker rm <container id>`
#### Example:
`docker rm 9faaefb4a255`

### Create and run a container (it'll download the image if it was not found locally):
`docker run <image>`
#### Example:
`docker run hello-world`

### Create and run a container, removing it afterwards:
`docker run --rm busybox date`

### Start a container:
`docker start <container id/name>`
#### Example:
`docker start 9faaefb4a255`

### Stop a container:
`docker stop <container id/name>`
#### Example:
`docker stop 9faaefb4a255`

### Pause a container:
`docker pause <container id/name>`
#### Example:
`docker pause 9faaefb4a255`

### Unpause a container:
`docker unpause <container id/name>`
#### Example:
`docker unpause 9faaefb4a255`

### Restart a container:
`docker restart <container id/name>`
#### Example:
`docker restart 9faaefb4a255`

### Attach terminal to a running container
`docker attach <container id/name>`
#### Examples:
```
docker attach 59c8b1bba36f
docker attach web
```
### Remove all containers at once! It pipes all containers id to the `docker rm` command:
`docker rm $(docker ps -aq)`

### Remove all exited containers:
`docker rm $(docker ps -qf status=exited)`

### Run a container assigning a name to it:
`docker run hello-world --name hello`

### Running a container in interactive mode:
`docker run -it <container id/name>`
#### Example:
`docker run -it centos /bin/bash`

### Pull all versions of an image from Docker Hub:
`docker pull -a <image>`
#### Example:
`docker pull -a ubuntu`

### Search all versions of an image from local store:
`docker images <image>`
#### Example:
`docker images ubuntu`

### Search all versions of an image on Docker Hub:
`docker search <image>`
#### Example:
`docker search mysql`

### Pull an image from Docker Hub with a specific version:
`docker pull <image>:<version>`
#### Example:
`docker pull ubuntu:16.04`

### Building an image based on a dockerfile:
If you are not on the same directory of the dockerfile, change the `.` to match the correct path to it:
`docker build -t my-busybox .`
It's a good practice to attach a tag on your new image. To do so, run this command instead:
`docker build -t my-busybox:latest .`
Now just create a container with your brand new image:
`docker run --rm my-busybox:latest`

### Exit container without killing it:
*A container contains a single process. If you kill this process, it'll have no more process running, killing the container as well. The command below make sure that the container will still be running after you detach your terminal from it:*

=> Press <kbd>Ctrl</kbd> + <kbd>P</kbd> + <kbd>Q</kbd>

## Dockerfile

### Examples (hopefully following the [Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/))
*Note:* To run the commands below to build the images and create the containers make sure you're on `dockerfiles` directory on this repository. If desired, a full path to the dockerfile can be specified.
All commands here:
* build an image based on a dockerfile
* create a container to run it
* remove the container
* remove the built image
Checkout the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more details about the *Dockerfile*.

#### 1) Create an image based on busybox:latest and show the current date:
```
FROM busybox:latest
MAINTAINER Helton Carlos de Souza <helton.development@gmail.com>
CMD ["date"]
```
##### Building and running it:
```
docker build -t h3170n/busybox-show-date:latest ./busybox-show-date/ && \
docker run --rm h3170n/busybox-show-date:latest && \
docker rmi h3170n/busybox-show-date:latest
```

#### 2) Create an image based on alpine:latest and print `Hello, World` to the console:
```
FROM alpine:latest
MAINTAINER Helton Carlos de Souza <helton.development@gmail.com>
ENTRYPOINT ["/bin/echo"]
CMD ["\"Hello, World\""]
```
##### Building and running it:
```
docker build -t h3170n/alpine-hello-world:latest ./alpine-hello-world/ && \
docker run --rm h3170n/alpine-hello-world:latest && \
docker rmi h3170n/alpine-hello-world:latest
```

#### 3) Create an image based on alpine:latest and print the distro version to the console:
```
FROM alpine:latest
MAINTAINER Helton Carlos de Souza <helton.development@gmail.com>
ENTRYPOINT ["/bin/cat"]
CMD ["/etc/lsb-release"]
```
##### Building and running it:
```
docker build -t h3170n/alpine-show-distro:latest ./alpine-show-distro/ && \
docker run --rm h3170n/alpine-show-distro:latest && \
docker rmi h3170n/alpine-show-distro:latest
```

#### 4) Create an image based on ubuntu:16.10 and install nginx:
```
FROM ubuntu:16.10
MAINTAINER Helton Carlos de Souza <helton.development@gmail.com>
RUN apt-get update && apt-get install -y nginx
```
##### Building and running it:
```
docker build -t h3170n/ubuntu-install-nginx:latest ./ubuntu-install-nginx/ && \
docker run --rm h3170n/ubuntu-install-nginx:latest && \
docker rmi h3170n/ubuntu-install-nginx:latest
```
