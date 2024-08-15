### 1. Docker Client Commands
#### Basic Commands:
- docker --version : Display the Docker version installed.
- docker info : Display system-wide information about Docker.
- docker help : Get help for Docker commands.
### 2. Docker Image Commands
#### Managing Images:
- docker images : List all Docker images on your system.
- docker pull [image-name] : Download an image from a registry.
- docker push [image-name] : Upload an image to a registry.
- docker build -t [image-name] . : Build an image from a Dockerfile.
- docker rmi [image-name] : Remove one or more images.
- docker tag [source-image] [target-image] : Create a new tag for an image.
- docker history [image-name] : Show the history of an image.
### 3. Docker Container Commands
#### Creating and Managing Containers:
- docker run [options] [image-name] : Run a new container.
- docker start [container-id] : Start one or more stopped containers.
- docker stop [container-id] : Stop one or more running containers.
- docker restart [container-id] : Restart a container.
- docker pause [container-id] : Pause all processes within a container.
- docker unpause [container-id] : Unpause a paused container.
- docker kill [container-id] : Kill a container by sending a signal to the main process.
- docker rm [container-id] : Remove one or more stopped containers.
- docker exec [container-id] [command] : Run a command in a running container.
- docker logs [container-id] : Fetch the logs of a container.
- docker inspect [container-id] : Display detailed information about a container.
- docker ps : List running containers.
- docker ps -a : List all containers (running and stopped).
- docker commit [container-id] [image-name] : Create a new image from a container’s changes.
- docker cp [container-id]:/path/to/file /local/path : Copy files from a container to the local filesystem or vice versa.
### 4. Docker Network Commands
#### Managing Networks:
- docker network ls : List all Docker networks.
- docker network create [network-name] : Create a new network.
- docker network rm [network-name] : Remove one or more networks.
- docker network inspect [network-name] : Display detailed information about a network.
- docker network connect [network-name] [container-id] : Connect a container to a network.
- docker network disconnect [network-name] [container-id] : Disconnect a container from a network.
### 5. Docker Volume Commands
#### Managing Volumes:
- docker volume ls : List all Docker volumes.
- docker volume create [volume-name] : Create a new volume.
- docker volume rm [volume-name] : Remove one or more volumes.
- docker volume inspect [volume-name] : Display detailed information about a volume.
- docker volume prune : Remove all unused volumes.
### 6. Docker Compose Commands
#### Managing Multi-Container Applications:
- docker-compose up : Build, create, start, and attach to containers for a service.
- docker-compose down : Stop and remove containers, networks, and volumes created by docker-compose up.
- docker-compose ps : List containers.
- docker-compose start : Start existing containers.
- docker-compose stop : Stop running containers without removing them.
- docker-compose restart : Restart containers.
- docker-compose logs : View output from containers.
- docker-compose build : Build or rebuild services.
- docker-compose exec [service-name] [command] : Execute a command in a running container.
- docker-compose scale [service-name]=[number] : Set the number of containers for a service.
- docker-compose pull : Pull the latest version of the image for a service.
### 7. Docker Swarm Commands
#### Managing Swarm Clusters:
- docker swarm init : Initialize a Swarm cluster.
- docker swarm join : Join a node to a Swarm as a manager or worker.
- docker swarm leave : Remove a node from the Swarm.
- docker node ls : List all nodes in the Swarm.
- docker node update : Update a node’s settings.
- docker service create : Create a new service in the Swarm.
- docker service ls : List services running in the Swarm.
- docker service rm : Remove a service from the Swarm.
- docker service update : Update a service in the Swarm.
- docker service scale [service-name]=[number] : Scale a service to the specified number of replicas.
### 8. Docker Registry Commands
#### Managing Docker Registries:
- docker login : Log in to a Docker registry.
- docker logout : Log out from a Docker registry.
- docker search [image-name] : Search for an image on Docker Hub or another registry.
### 9. Docker System Commands
#### Managing Docker System Resources:
- docker system df : Show Docker disk usage.
- docker system prune : Remove unused data (containers, networks, images, etc.).
- docker system info : Display detailed information about the Docker system.
- docker system events : Get real-time events from the Docker Daemon.
### 10. Advanced Docker Commands
#### For Advanced Users:
- docker buildx : Build images with advanced features like multi-platform builds, distributed builds, etc.
- docker context : Manage Docker contexts, which allow you to switch between different Docker environments (e.g., local, remote).
- docker secret : Manage sensitive data (like passwords) in Docker Swarm.
- docker config : Manage configuration data that can be used by services in Docker Swarm.
