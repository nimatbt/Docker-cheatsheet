# Docker-cheatsheet

## DWS-OPS-005-Docker

### 1) Get mysql:8 image and specify ports, volumes and docker version by which the image is built.

Get mysql:8 image

- docker pull mysql:8

Show docker version, ports and volumes

- docker image inspect mysql:8

### 2) Get nginx:latest image and save it to a local file. then load it using load and import commands.

Get nginx:latest image and save it to a local file

- docker pull nginx:latest
- docker image save -o nginx.tar nginx:latest

load and import file:

- docker load -i nginx.tar    
- docker import nginx.tar nginx:mynginx


### 3) Run a nginx container and bind Exposed Port (80) to port 8081 of the host.

- docker run -d --name mynginx -p 8081:80 nginx:latest

### 4) Find the number of running processes of the container run in the task number 3.

- docker top mynginx

### 5) What is docker proxy?

The docker-proxy operates in userland, and simply receives any packets arriving at the host's specified port,
 that the kernel hasn't 'dropped' or forwarded, and redirects them to the container's port.
 
### 6) What are dangling images and how to remove them?

Dangling images are layers that have no relationship to any tagged images.

- docker image prune
