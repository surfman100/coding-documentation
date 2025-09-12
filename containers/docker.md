# Docker 
Consists of:
- service/daemon **dockerd**  
- apis  
- cli client **docker** 

**Kubernetes** - Open source, container orchestration system.

VM v Container: VM has its own kernel, drivers etc. lot of overhead

## Installation  
Docker Desktop handles all the nitty gritty of setup for your OS and encapsulates above.  
includes:
- daemon  
- client  
- compose   
- content trust  
- kubernetes  
- credential helper  

opening the desktop starts the service etc.

## Concepts

| Concept | Description |

| --- | --- |
| Image | *read only* template (package). what to install and configuration |
| DockerFile | listing of steps to create a template. creates layers |
| container | runnable instance of container. api/cli to start/stop/move/new image off state |

## Commands 

```
#get latest ubuntu image
docker pull ubuntu 

#list images
docker images

#build image
docker build -t billtierney/first

docker push billtierney/first

```

## Docker Compose  
The YAML file that defines multiple containers/services:
- image(s) to use (node, vite, mysql, phpmysqladmin, traefix)
- volume(s) to persist data
- proxy if needed
- each service

```
docker compose watch

docker compose up

docker compose down --volumes
```

Amazing quick hotload.

**Docker file** - instructions to build an image from layers
**Compose file** - references docker files to build an image for a service  

## Docker File Internals
made up of layers  
each layer is put into its own subdirectory  
running on container from image a union filesystem is created, layers stacked  
two dirs -> union filesystem & a run directory 

**Create a new image layer**  
make a change in a running container and then in another terminal execute:
```
docker container commit 
```

**Full Process**
Create a Dockerfile  
Build it
Tag it
Push it

Playground [here](https://labs.play-with-docker.com/?_gl=1*13rprn6*_gcl_au*MTU1MjU0NDg5Ny4xNzU3NDMwNDcw*_ga*MzA0MTIwODM2LjE3NTc0MzAwNTQ.*_ga_XJWPQMJYHQ*czE3NTc2ODY3OTkkbzckZzEkdDE3NTc2ODkyNzYkajYwJGwwJGgw)  
have a look at [Networking](https://docs.docker.com/engine/network/#published-ports)

left off here:
https://docs.docker.com/get-started/workshop/04_sharing_app/