# Docker

Docker is a container management platform. It is based on 3 important things

- Images
- Containers
- Volumes

Please reference the [official docker documentation](https://docs.docker.com/) for better understanding.


#### Images

Images are software that are shipped to be used in docker by companies and developers. Images can be used to install / clone softwares.

#### Containers

Containers are mini enviornments which are independent of each other can run the softwares that are provided in the images

#### Volumes



## Commands

Checking the docker version

```shell
docker -v
docker --version
```

To get more in detail version information about parts of docker

```shell
docker version
```

### List all the containers

```shell
docker ps
```

This command will list all the running containers, we can also give `-a` flag to also display the stopped containers along with the running containers

### Running a container

```shell
docker run ubuntu
```

This will run the ubuntu docker image, we also have different options / flags that we can pass

- `--name SOMENAME` : this flag gives your container a unique name which can be used to identify it

- `-it` : assigns an interactive shell to talk with the docker container

- `-d` : (detach) makes the docker container work in the background without having to keep the terminal on

- `-e PASSWORD='SomePassword'` : pass environment variables

### Running older versions

When we run the container without specifying the image version, it pulls the latest version but if we want to run some older version, we can do it by specifying the version after the image name

```shell
docker run ubuntu:22.04
```

### Stopping a container

```shell
docker stop <CONTAINER ID OR NAME>
```

This command will stop the container , it will not be removed, only stopped


### Remove a container

```shell
docker rm <CONTAINER ID OR NAME>
```

### Remove all stopped containers

```shell
docker container prune
```

This command will remove all the stopped containers from the system

### Removing all unused resources


```shell
docker system prune
```

This will remove all the unused images, stopped containers, etc


### Mapping a port

To specify a port that we want our service to be accessible on or instead it will use the default port


```shell
docker run -p <OUTER-PORT>:<INNER-PORT> mongo
```

The OUTER-PORT is the port which we will be using to access the service on our local machine

The INNER-PORT is the internal port of the image which will pe mapped


### Logs

```shell
docker logs CONTAINER-NAME
```

We can also use the `CONTAINER-ID` instead of `CONTAINER-NAME`


## Docker Compose

The `docker compose` is a better way to run containers

The docker compose command uses `.yml` files for getting information about containers that need to be run

```yaml
version: "3"
services:
    mongodb:
        image: mongo
        ports:
            - "27017:27017"
        environment:
            - MONGO_INITDB_ROOT_USERNAME:admin
            - MONGO_INITDB_ROOT_PASSWORD:password
    mongo-express:
        image: mongo-express
        restart: always
        ports:
            - "8081:8081"
        depends-on:
``` 

## Dockerfile 

`Dockerfile` is the file that contains information about building the image, this file is used to build the docker image when run the `docker build` command

Let's see what all options do we get in a docker file

### Base image

```
FROM node:tag
```
This installs the node in our image

### Environment Variables

```
ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PASSWORD=Password
```

### Run linux commands

```
RUN mkdir /home/app
```

### Copy files

```
COPY . /home/app
```

This command is used to copy files from the host to the image, the first param `.` tells that we want to copy all the file from the host's current dir to `/home/app` in the image


### Execute an entrypoint

```
CMD ["node", "server.js"]
```

We can have only on entrypoint command in the Dockerfile