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

### Run a command in a container (it'll download the image if it was not found locally):
`docker run <image>`
#### Example:
`docker run hello-world`

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

### Pull an image from Docker Hub with a specific version:
`docker pull <image>:<version>`
#### Example:
`docker pull ubuntu:16.04`

### Exit container without killing it:
*A container contains a single process. If you kill this process, it'll have no more process running, killing the container as well. The command below make sure that the container will still be running after you detach your terminal from it:*

=> Press `Ctrl` + `P` + `Q`
