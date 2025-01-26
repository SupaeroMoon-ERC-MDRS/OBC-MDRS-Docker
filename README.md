# OBC-MDRS-Docker
This repo contains docker files for building the Ubuntu 22.04 raspberry pi docker container

## Setup
After [installing Docker](https://docs.docker.com/engine/install/raspberry-pi-os/) on the board, transfer this repo files in the local file system of the board.

NOTE: It is required to know set up the connection and know IP address of the Raspberry for the following step.

### File copy
Use *scp* on your local machine to transfer files towards the board, using the command:


```bash
scp -r OBC-MDRS-Docker/src/ supaeromoon@<rasp-ip>:/
```

or by cloning this repo:

```bash
git clone https://github.com/SupaeroMoon-ERC-MDRS/OBC-MDRS-Docker
```

### Build container (environment)
Then build and run the container having the container terminal available, by using the file ```docker-compose.yml``` that calls ```Dockerfile``` to build the container in the first place, using the command: 

```bash
cd Docker
docker compose up -d 
```
or 
```bash
cd Docker
docker run --platform linux/arm64 -it docker-rasp # if running from docker desktop windows
```

For development on architectures different than **arm64** edit the ```docker-compose.yml``` file, dependent on the host platform. This step isn't necessary if you're running docker desktop.

### Visual Studio Code Dev Container
Moreover is possible to run the container through [Visual Studio Code Dev Containers](https://www.youtube.com/watch?v=dihfA7Ol6Mw), having the container environment identical to the local environment. Follow the instructions and make sure to *Reopen in container* in ```src``` folder.
