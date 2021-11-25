---
layout: post
title: "List of commands used to work with Docker"
date: 2021-11-24 22:00:00 -0300
categories: tutorial linux docker
---
Follow [the official documentation](https://docs.docker.com/engine/install/ubuntu/) to install Docker Engine.

## Basic commands

```bash
# Alias for docker container ls
docker ps

# List all dead containers
docker ps -a

# Run a command in a new container
docker run --name box1 -d -p 8080:80 nginx

# Get IP of container
docker inspect box1 | grep IPAddress

# Remove a container
docker rm -f box1

# Remove a docker image
docker rmi nginx

# Run container from image busybox for 1 hour and die
docker run -d --name box1 busybox sleep 3600

# Run a command (mkdir test) in a running container
docker exec box1 mkdir test

# Run a command in a runnning container on iteractive mode
sudo docker exec -it box1 sh

# Display a live stream of container(s) resource usage statistics
docker stats

# Stop(die) a container
docker stop box1

# Start a container
docker start box1

# Show all logs of container
docker logs box1

# List all images locally
docker images

# Download docker image from repository
docker pull busybox

# Create new docker image from a dead container
docker commit --author="ailtonbsj" --message="Image with commit" box1 image1

# Create a tag for docker image
docker tag image1 ailtonbsj/image1:1.0

# Send image to online repository
docker login
docker push ailtonbsj/image1:1.0

# Export container as a tar file
docker export box1 > box1.tar

# Export docker image as a tar file
docker save image1 > box1.tar

# Import tar file as a docker image
cat box1.tar | docker import - image2

# Create volume for docker
docker volume create myVol

# List all volumes
docker volume ls

# Inspect volume
docker volume inspect myVol

# Run a container with volume mounted
docker run -d -p 81:80 --name box1 --mount source=myVol,target=/usr/share/nginx nginx

# Run a container with bind mount
docker run -d -p 81:80 --name box2 -v ~/html:/usr/share/nginx/html nginx

# Run a container with tmpfs
docker run -d --name box3 --mount type=tmpfs,destination=/cache,tmpfs-size=1000000 busybox sleep 3600

# Limit use of RAM memory
docker run -d --memory 10m busybox sleep 3600

# Limit use of CPUs
docker run -d --cpus=0.5 progrium/stress -c 8 -t 30s
```

## Docker Network commands

```bash
# List all networks
docker network ls

# Create net network
docker network create -d bridge petsBridge

# Create containers using network in bridge mode
docker run -d --net petsBridge --name db consul
docker run -d --env "DB=db" --net petsBridge --name web -p 8000:5000 chrch/docker-pets:1.0

# Create containers using network in host mode
docker run -d --net host --name db consul
docker run -d --env "DB=localhost" --net host --name web chrch/docker-pets:1.0
```

## Docker Swarm commands

```bash
# Provisioning docker as MASTER
docker swarm init --advertise-addr <IP_OF_VM>

# Join some VM to cluster
docker swarm join --token <MASTER_TOKEN>

# Create containers using network in overlay mode
docker network create -d overlay petsOverlay

# Create service in docker node Master
docker service create --network petsOverlay --name db consul
docker service create --network petsOverlay --name web -p 8000:5000 -e "DB=db" chrch/docker-pets:1.0

# List service on cluster of dockers (Swarm)
docker service ls

# Replicate service on nodes
docker service scale web=3
```

## Other util commands

```bash
# List all port used
netstat -nltp

# Create zero-file with 1MB
dd if=/dev/zero of=file.0 bs=1024 count=1024
```

# Docker Compose and Dockerfile

See [this project](https://github.com/ailtonbsj/dio-docker-101) created on Digital Innovation One / TQI Bootcamp.