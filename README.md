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

#### Docker Practice
- Name: Nima Tabatabaee
- Grops: Bladrina
- Practice Name: Ops-005-Docker
-                Ops-006-Docker
- [@dwsclass](https://github.com/dwsclass) dws-ops-005-Docker

Copyright 2022 Nima Tabatabaee <nima.tabatabaee@gmail.com>
