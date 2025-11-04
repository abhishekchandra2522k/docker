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
- `docker run -d -P -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:5.7`: -e tag is used to pass the export variables
- `docker pull <image name>`: to pull an image from the container registry (remote)
- `docker inspect <image name>/<container name/id>`: to see the json information of the image/container - main is the config block where we have entry point and other service specific commands, we can also find the port on which the process is running and volume path information.
- `docker logs <container id / name>`: to check the logs and troubleshoot, we don't see the output to the cmd `docker run` in the console as in the backend entrypoint and other "service" specific commands are triggered which are mentioned in the config block of the inspect file. we can see the output of these commands using docker logs cmd.
- `docker volume create <volume name>`: to create a new docker volume, stores data in the host machine at `/var/lib/docker/volumes/<volume name>/_data/`. in case the container gets removed, we can attach the volume to a new container preserving the data.
- `docker volume ls`: to view all the available docker volumes
- `docker build -t <provide a new image name> <Dockerfile path>`: to create a new image fromt the Dockerfile
  - Example: `docker build -t titanimg .`

## concepts

- bind mount: it is used to inject data from the host machine to the container, usually developers code in the host machine and that gets synced to the container
  - `docker run --name vprodb -d -e MYSQL_ROOT_PASSWORD=mypass -p 3030:3306 -v /home/ubuntu/vprodbdata:/var/lib/mysql mysql:5.7`: this is an example command to run a mysql container with bind mount.
- volume mount: for preserving data, better option is volumes.
  - `docker volume create mydbdata`: to create a volume with the name mydbdata
  - `docker run --name vprodb -d -e MYSQL_ROOT_PASSWORD=mypass -p 3030:3306 -v mydbdata:/var/lib/mysql mysql:5.7`: we pass the volume name in place of the host bind mount path to attach a volume to the container directory.

## Dockerfile

- FROM: Base Image (Offical Images recommended)
- LABELS: Adds metadata to an image
- RUN: execute commands in a new layer and commits the results
- ADD/COPY: copy or add a file into the image
- CMD: run binaries/commands on docker run
- ENTRYPOINT: allows us to configure a container that will run as an executable
- VOLUME: creates a mount point and marks it as holding externally mounted volumes
- EXPOSE: container listens on the specified network ports at runtime
- ENV: sets the environment variables
- USER: sets the username (or UID)
- WORKDIR: sets the working directory
- ARG: defines a variable that users can pass at build-time
- ONBUILD: adds to the image a trigger instruction to be executed at a later time
