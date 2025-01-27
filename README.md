# OBC-MDRS-Docker
This repo contains docker files for building the Ubuntu 22.04 raspberry pi docker container


## Docker setup for Raspberry pi
After [installing Docker](https://docs.docker.com/engine/install/raspberry-pi-os/) on the board, transfer the files in directory ```/src/rpi_MDRS/Docker``` in the local file system of the board.

NOTE: It is required to know set up the connection and know IP address of the Raspberry for the following step.

Use *scp* on your local machine to transfer files towards the board, using the command:


```bash
scp -r OBC-RPI-MDRS/src/rpi_MDRS/Docker supaeromoon@<rasp-ip>:/
```

Then build and run the container having the container terminal available, by using the file ```docker-compose.yml``` that calls ```Dockerfile``` to build the container in the first place, using the command: 

```bash
cd Docker
docker compose up -d
docker run --platform linux/arm64 -it docker-rasp # if running from docker desktop windows
```

For development on architectures different than **arm64** edit the ```docker-compose.yml``` file, dependent on the host platform. This step isn't necessary if you're running docker desktop.

Moreover is possible to run the container through [Visual Studio Code Dev Containers](https://www.youtube.com/watch?v=dihfA7Ol6Mw), having the container environment identical to the local environment.

# Useful docker commands:

## General commands:
- **List all running containers**:
  ```bash
  docker ps
- **List all containers**:
  ```bash
  docker ps -a
- **List all Docker images:**:
  ```bash
  docker images
- **Stop a running container:**:
  ```bash
  docker stop <container_name_or_id>
- **Start a stopped container:**:
  ```bash
  docker start <container_name_or_id>
- **Remove a container:**:
  ```bash
  docker rm <container_name_or_id>
- **Remove an image:**:
  ```bash
  docker rmi <image_name_or_id>

## Build and Run Containers
- **Build a Docker image from a Dockerfile:**:
  ```bash
  docker build -t <image_name>:<tag> .
- **Run a container interactively:**:
  ```bash
  docker run -it <image_name>:<tag>
- **Run a container in detached mode:**:
  ```bash
  docker run -d <image_name>:<tag>
- **Run a container with a specific name:**:
  ```bash
  docker run --name <container_name> <image_name>:<tag>
- **Run a container and bind a port:**:
  ```bash
  docker run -p <host_port>:<container_port> <image_name>:<tag>
## Accessing Running Containers
- **Attach to a running container:**
  ```bash
  docker attach <container_name_or_id>
- **Open a new shell session in a running container:**
  ```bash
  docker exec -it <container_name_or_id> /bin/bash
- **View container logs:**
  ```bash
  docker logs <container_name_or_id>
- **Follow live logs of a container:**
  ```bash
  docker logs -f <container_name_or_id>

## Cleaning Up:
- **Remove all stopped containers:**
  ```bash
  docker container prune
- **Remove all unused images:**
  ```bash
  docker image prune
- **Remove all unused images, containers, and volumes:**
  ```bash
  docker system prune

## Debugging Containers:
- **Inspect a container's details:**
  ```bash
  docker inspect <container_name_or_id>
- **Check a container's resource usage:**
  ```bash
  docker stats <container_name_or_id>
- **Check network details:**
  ```bash
  docker network inspect <network_name>

## Saving and Sharing:
- **Save a Docker image to a tar file:**
  ```bash
  docker save -o <file_name>.tar <image_name>:<tag>
- **Load a Docker image from a tar file:**
  ```bash
  docker load -i <file_name>.tar
- **Push an image to Docker Hub:**
  ```bash
  docker push <username>/<image_name>:<tag>
## Docker Compose:
- **Start services in the background using `docker-compose.yml`:**
  ```bash
  docker-compose up -d
- **Stop services:**
  ```bash
  docker-compose down
- **View logs for services:**
  ```bash
  docker-compose logs
- **Rebuild services:**
  ```bash
  docker-compose up --build