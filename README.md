# Docker-cheatsheet

### DWS-OPS-005-Docker

#### 1) Get mysql:8 image and specify ports, volumes and docker version by which the image is built.

```
Get mysql:8 image

- docker pull mysql:8

Show docker version, ports and volumes

- docker image inspect mysql:8
```

#### 2) Get nginx:latest image and save it to a local file. then load it using load and import commands.

```
Get nginx:latest image and save it to a local file

- docker pull nginx:latest
- docker image save -o nginx.tar nginx:latest

load and import file:

- docker load -i nginx.tar    
- docker import nginx.tar nginx:mynginx
```

#### 3) Run a nginx container and bind Exposed Port (80) to port 8081 of the host.

```
- docker run -d --name mynginx -p 8081:80 nginx:latest
```

#### 4) Find the number of running processes of the container run in the task number 3.

```
- docker top mynginx
```

#### 5) What is docker proxy?

```
The docker-proxy operates in userland, and simply receives any packets arriving at the host's specified port,
 that the kernel hasn't 'dropped' or forwarded, and redirects them to the container's port.
 ```
 
#### 6) What are dangling images and how to remove them?

```
Dangling images are layers that have no relationship to any tagged images.

- docker image prune
```

#
### DWS-OPS-006-Docker

#### 1) Which signal will send to a running container, when the container killed?

```
SIGKILL

docker kill [CONTAINER-NAME]
```

#### 2) Create a container from alpine image,then install nginx on it and create an image from it.

```
1) in the host: 
docker run -it --name myalpine alpine:latest 
2) In the container:
apk add nginx 
3) in the host: 
docker commit myalpine alpine:nginx
```

#### 3) What happened to processes of a container when it pauses?

```
The container stays running and uses memory but does not use the processor
```

#### 4) Run a container from redis image and send it's id to myredis.cid file

```
docker run -d --name myredis redis:latest
docker inspect myredis -f '{{ .Id }}' > myredis.cid
```

#### 5) Run a container from nginx with the following specifications
- Memory=512M
- Sawp=256m
- Cpus=0,2
- Cpu=1.5 core


```
docker run -d --name mynginx --memory 512m -memory-swap 768m --cpuset-cpus 0,2 --cpus 1.5 - nginx:latest
```

#### 6) Run a container from alpine and set CLASS=dws and NAME=nima environment variables in it. Then run env command in container and show them.

```
docker run -it --name myalpine --env CLASS=dws --env NAME=Nima alpine:latest
- inside Container:
# echo Name=${NAME} and Class=${CLASS}
``` 

#### 7) Run a container from alpine and mount a directory from your host to /data in the container and change working dir to that path.

```
docker run -it --name myalpine -v /home/mydata:/data -w /data alpine:latest
```

#
### DWS-OPS-007-Docker

#### 1) What is Dockerfile?

```
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession
```

#### 2) Difference between docker commit and docker build command

```
- The docker build command builds Docker images from a Dockerfile
- Docker's commit command allows users to take a running container and save its current state as an image
```

#### 3) Difference between ENV and ARG

```
- ENV is for future running containers. ARG for building your Docker image. ENV is mainly meant to provide default values for your future environment variables.
- ARG values are not available after the image is built. A running container won’t have access to an ARG variable value
```

#### 4) Difference between CMD and ENTRYPOINT

```
- CMD sets default command and/or parameters, which can be overwritten from command line when docker container runs
- ENTRYPOINT command and parameters will not be overwritten from command line unless you add the --entrypoint flag. Instead, all command line arguments will be added after ENTRYPOINT parameters
```

#### 5) Difference between Expose and Publish ports

```
Exposing ports is a way of documenting which ports are used, but does not actually map or open any ports. Exposing ports is optional. You publish ports using the --publish or --publish-all flag to docker run . This tells Docker which ports to open on the container's network interface
```

#### 6) What does it mean when we use the FROM in Dockerfile?

```
The FROM in dockerfile means the file system of that operating system(rootfs), not a complete operating system(bootfs+rootfs)
```

#### 7) Difference between RUN and ENTRYPOINT

```
- RUN executes command in a new layer and creates a new image. E.g., it is often used for installing software packages.
- ENTRYPOINT configures a container that will run as an executable.
```

#### 8) Difference between ADD and COPY

```
- COPY takes in a src and destination. It only lets you copy in a local file or directory from your host (the machine building the Docker image) into the Docker image itself.
- ADD lets you do that too, but it also supports 2 other sources. First, you can use a URL instead of a local file / directory. Secondly, you can extract a tar file from the source directly into the destination
```

#### 9) What is the purpose of VOLUME in Dockerfile

```
You can declare it in a Dockerfile, which means each time a container is started from the image, the volume is created, even if you don't have any -v option
```


#### Docker Practice
- Name: Nima Tabatabaee
- Grops: Bladrina
- Practice Name: Ops-005-Docker,
                 Ops-006-Docker,
                 Ops-007-Docker
- [@dwsclass](https://github.com/dwsclass) dws-ops-005-Docker
- [@dwsclass](https://github.com/dwsclass) dws-ops-006-Docker
- [@dwsclass](https://github.com/dwsclass) dws-ops-007-Docker

Copyright 2022 Nima Tabatabaee <nima.tabatabaee@gmail.com>
