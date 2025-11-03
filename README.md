# docker

## docker commands

- `docker ps`: see the running containers
- `docker images`: see the pulled images
- `docker ps -a`: see all the containers (running and stopped)
- `docker start <name/id of the container>`: to start a stopped container
- `docker run <image name>`: to create a new container from the image (it will also pull the image from the container registry in case the image doesn't exist in the local)
- `docker run -d <image name>`: to run the conntainer in the detached mode
- `docker run -d -P <image name>`: to run the container in the detached mode and map the service port to the available container port
- `docker run -d -p 7080:80 nginx`: to run a container in the detached mode and map the specific available port of the container to the port on which the process/service is running, example nginx runs on port 80 and we mapped 7080 port. we can access nginx service via `<ip>:7080`.
- `docker pull <image name>`: to pull an image from the container registry (remote)
- `docker inspect <image name>`: to see the json information of the container - main is the config block where we have entry point and other service specific commands
- `docker logs <container id / name>`: to check the logs and troubleshoot, we don't see the output to the cmd `docker run` in the console as in the backend entrypoint and other "service" specific commands are triggered which are mentioned in the config block of the inspect file. we can see the output of these commands using docker logs cmd.
