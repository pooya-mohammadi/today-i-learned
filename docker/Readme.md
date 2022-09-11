# Docker & Docker-Compose
How to add environment variables to docker run
```
docker run .... -e cam_ip=0 -e cam_ip_2=1
```

```
#dockerfile
ENV DATABASE_URL=0
```

## Install Docker engine[Main Installation Process] 

```
sudo rm -rf /var/lib/containerd/
sudo rm -rf /var/lib/docker/
sudo apt-get purge -y docker-ce docker-ce-cli docker.io containerd.io

# Install 
 sudo apt-get update

 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
# make sure the section gets done. Adding freedomofdevelopers helped me once.

sudo apt-get install docker-ce docker-ce-cli containerd.io -y
# Turn on and off your VPN
```

Easy way, but does not always install the stable version:

```
sudo snap install docker
```

Install Docker Compose

```
# turn off your VPN or freedomofdevelopers
sudo apt install docker-compose -y
```

Enable Docker

```
sudo systemctl enable docker
sudo systemctl start docker
```

Start the Docker daemon 

```
sudo systemctl start docker
sudo service docker start
```

 how to restart docker linux 

```
sudo systemctl start docker
```

docker restart 

```
sudo systemctl restart docker
```

How to start docker

```
systemctl start docker.service
#(OR)
systemctl start docker
# it will start docker
```


Verify

```
# turn on your vpn
sudo docker run hello-world
```

Verify Docker-Compose

```
docker-compose --version
```


Nvidia

```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update
sudo apt-get install -y nvidia-docker2
sudo systemctl restart docker
sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi
```


Errors:


     Docker Pull limit:

	    You need to sign in to docker hub.

How to Login

run the below code in terminal:
```
sudo docker login
```
It will ask for your username
then for your password
At the end:
```
Login Succeeded
```

Dockerfile:
	- Dockerfile cannot have more than one CMD and it's the only command which will be run
		- If you need more commands you can stack them in a bash file and run the bash file through the CMD 
		- If you need to run a service among your commands, you can add an & to the end of that command so it will run in the background
		- To keep the container alive you need to have a running process on it, if the last command of your bash file is not a service, the container will die. Preventing it is possible through a while true at the end of your commands
	- Best Practice:
		- It's better to assign multiple 

## How to run docker without Sudo:

run in terminal
```
sudo setfacl -m user:<user>:rw /var/run/docker.sock
# or
sudo setfacl -m user:$USER:rw /var/run/docker.sock

# best approach
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
# reference: https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user
```

Docker commands:
How to get into a docker image:
```
docker -it image-name
```

How to get into a live container and get access to the bash:
```
docker exec -it container-id bash
```

How to remove images:
```
docker rmi image-ids
```

How to remove all the images:
```
docker image prune -a
```

How to copy from docker container a file to local
```
docker cp container_name(or id):file_path local_path
```

Docker limit resource:
How to be able to configure:
```
sudo nano /etc/default/grub
```

```
GRUB_CMDLINE_LINUX="cdgroup_enable=memory swapaccount=1"
```

```
sudo update-grub
```
Reboot.

How to get inside a docker image:
```
sudo docker run -it --name container-name docekr-image:tag bash 
# bash will be run as a command and it will open the bash.
# Whatever comes after the docker image name is a command.
```
Memory(RAM):
```
sudo docker run -it --memory=”1g” --memory-reservation=”750m” --memory-swap=”2g” ubuntu
```
memory: max limit memory 
memory-reseervation: actual granted
memory-swap: swap like usual ubuntu

CPU:
```
sudo docker run -it --cpus=”1.0” ubuntu
```

Storage:
```
$ docker run -it --storage-opt size=120G ubuntu
```

How to run docker without sudo on ubuntu
```
sudo setfacl -m user:$USER:rw /var/run/docker.sock
```

How to print the logs of a container
```
docker container logs container-id
```

How to ignore files from docker:
```
You need a file called .dockerignore
```

What does the slim tag refer to?
```
slim tag after python is used to decrease the size of the python image for the tools that are needed. No more.
Buster is the codename of a stable Debian release of 10.4.
python buster is very huge almost 900 megabytes
```
references: https://medbusterium.com/swlh/alpine-slim-stretch-buster-jessie-bullseye-bookworm-what-are-the-differences-in-docker-62171ed4531d

What is alpine:
```
It's an ubuntu distribution and it's much smaller than the usual ubuntu 
```


The bottom line is: 
Don't use Alpine Linux for python images
references:
	https://pythonspeed.com/articles/alpine-docker-python/
	https://pythonspeed.com/articles/official-python-docker-image/

How to time a build process:
```
time docker build -t ubuntu-gcc -f Dockerfile.ubuntu --quiet .
```

How to create a docker image:
```
docker build -t pooyamohammadi/torch_cpu:3.9-buster .
```

How to force docker to create a clean image:
```
docker build --no-cache -t u12_core -f u12_core .
```

how to push an image to docker-hub:
```
docker image tag project-name USER/project-name:latest # USER is the username on docker-hub
docker image push USER/project-name:latest # latest or tag label
```

How to stop a container after exiting:
```
docker run --rm --name container-name image-name
```

How to save and export an image
```
sudo docker save ubuntu > ubuntu_save.tar
sudo docker export ubuntu > ubuntu_export.tar
```

How to commit a container as an image
```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

Why --no-cache-dir:
Using it the python libraries will not be cached after installation in 
```
RUN pip install --no-cache-dir -r requirements.txt
```

What is EntryPoint in dockerfile:
```
It exactly is like CMD. Both can be modified at run time. sudo docker run ubuntu bash or ... (the last bash overwrites the CMD of ubuntu image)
The Entrypoint is more robust than CMD. EntryPoint is recommended for images that are not supposed to modify by users.
Combining ENTRYPOINT and CMD allows you to specify the default executable for your image while also providing default arguments to that executable which may be overridden by the user.
```
references: https://www.ctl.io/developers/blog/post/dockerfile-entrypoint-vs-cmd

What is EXPOSE:
```
It's like a hint that the code will be exposed on that port. It's used inside the dockerfile. Whether setting it or not won't change it. 
Neither specify EXPOSE in dockerfile nor -p in commandline – Container would be accessible inside a host machine but not on host ip:port
Only specify EXPOSE in dockerfile – You expose ports using the EXPOSE keyword in the Dockerfile or the –expose flag to docker run. Exposing ports is a way of documenting which ports are used, but does not actually map or open any ports. Exposing ports is optional. You stil be able to access a container from inside a host.
Specify EXPOSE in dockerfile and -p in commandline – If you EXPOSE and -p a port, the service in the container is accessible from anywhere, even outside Docker host.

If you do -p, but do not EXPOSE –
EXPOSE is a way of documenting
-publish (or -p) is a way of mapping a host port to a running container port.

One benefit of using the EXPOSE instruction, whether you are running a multi-container application or not, is that it helps others understand what port the application listens by just reading the Dockerfile without the need of going through your code.

EXPOSE 80:UDP # means it will listen on udp protocol

How EXPOSE and –expose[It's used inside docker-compose] work?

Basically, EXPOSE is a documentation mechanism that gives configuration information another command can use, provides a hint about which initial incoming ports will provide services, or informs the decisions that the container operator makes. EXPOSE does not provide much networking control to an image developer. 

As earlier explained, you can use the –expose flag in a Docker run string to add to the exposed ports.

By default, the EXPOSE instruction does not expose the container’s ports to be accessible from the host. In other words, it only makes the stated ports available for inter-container interaction. 

For example, let’s say you have a Node.js application and a Redis server deployed on the same Docker network. To ensure the Node.js application communicates with the Redis server, the Redis container should expose a port. 

If you check the Dockerfile of the official Redis image, a line is included that says EXPOSE 6379. This is what allows the two containers to talk with one another. 

Therefore, when your Node.js application connects to the 6379 port of the Redis container, the EXPOSE directive is what ensures the inter-container communication takes place.
```


Publishing Docker ports via -P or -p

```
There are two ways of publishing ports in Docker:
- Using the -P flag
- Using the -p flag
Let’s talk about each of them. 
a) Using the -P flag
Using the -P (upper case) flag at runtime lets you publish all exposed ports to random ports on the host interfaces. It’s short for –publish-all.
As earlier mentioned, EXPOSE is usually used as a documentation mechanism; that is, hinting to the container operator about the port(s) providing services.
Docker allows you to add -P at runtime and convert the EXPOSE instructions in the Dockerfile to specific port mapping rules.
Docker identifies all ports exposed using the EXPOSE directive and those exposed using the –expose  parameter. Then, each exposed port is mapped automatically to a random  port on the host interface. This automatic mapping also prevents  potential port mapping conflicts.
b) Using the -p flag
Using the -p (lower case) flag at runtime lets you publish a container’s specific port(s) to the Docker host. It’s short for –publish.
It allows you to map a container’s port or a range of ports to the host explicitly—instead of exposing all Docker ports.
Note that irrespective of the EXPOSE instructions in the Dockerfile, using the -p flag at runtime allows you to override them.

p or P is used to connect docker with host, Expose and expose is used to grant inter-container connection.
```

How to see the history of a docker image:
```
sudo docker history <image-name>
```

Difference between ADD and COPY:
```
They kind of do the same but the COPY is saved a layer inside the docker image history and if you want to add a big file it will increase the size of the docker image no matter you remove the file or folder or not.
On the other hand, Add is not saved as a layer and it wont increase the model size.
```

How to restart docker:
```
If you have installed it using snap:
sudo snap start docker
```

How to install torch-cpu on docker
```
pip3 install --no-cache-dir torch==1.10.0+cpu torchvision==0.11.1+cpu -f https://download.pytorch.org/whl/torch_stable.html
```

What is the restart in docker-compose:
```
You can set a container to restart: always or set restart on-failure to restart after any failures.
```

The order of a docker file:
```
The things that are more likely to change should be lower on the list and the ones that are less likely to change should be higher on the list.
The docker image is full of layers the if you change a layer frequently and it happens to be in the first section of your docker image, guess what happens. All the layers that are following it will be re-installed again.
```

Docker multi-stage build:
Why and how do I need a multi-stage build:
```
If you want to build a go file and want to show it in an alpine version of Linux you don't need to use a GO image. It's highly weighted and it's overkill for this purpose. Let see an example:

FROM golang:1.16 AS build
ADD . /src
WORKDIR /src
RUN go test --cover -v ./...
RUN go build -v -o demo



FROM alpine:3.4
EXPOSE 8080
CMD ["demo"]
COPY --from=build /src/demo /usr/local/bin/demo
RUN chmod +x /usr/local/bin/demo

$$$$$$$$$$$$$$$$$
The final image is about 17 megabytes because only the first image will be contained and the other ones will be discarded.
```
references: https://www.youtube.com/watch?v=zpkqNPwEzac

How to remove volumes:
```
sudo docker volume rm mlflow_artifact mlflow_dbdata
```

How to list volumes:
```
sudo docker volume ls
```

How to search a docker image
```
sudo docker search docker-name
```

Bind Mount:
```
It's not controlled by docker and that's why it's more preferred for online processing demands.
If the mounted file does not exist on the container host the docker will through an error

```


CMD vs EntryPoint:
```
CMD echo "Hello World" (shell form)
CMD ["echo", "Hello World"] (exec form)
ENTRYPOINT echo "Hello World" (shell form)
ENTRYPOINT ["echo", "Hello World"] (exec form)
# However, try to keep all your instructions in exec form to prevent potential performance issues.
# The CMD instruction is only utilized if there is no argument added to the run command.
# ENTRYPOINT is the other instruction used to configure how the container will run. 
# What is the difference between CMD and ENTRYPOINT: You cannot change the entrypoint instruction by adding arguments to the run command. You make sure that the image is built specifically for a certain use.
```

How to add environment arguments to docker run:
```
sudo docker run 
-e POSTGRES_USER='postgres' \
-e POSTGRES_PASSWORD='password' docker_image_name
```

How to mount a file with docker run:
```
sudo docker run -it --mount type=bind,source=/home/ai/projects/medical/openvino/,target=/openvino ubuntu:20.04 bash
```

How to open up interactive shell using docker-compose:
```
version: "3"
services:
  app:
    image: app:1.2.3
    stdin_open: true # equivalent to docker run -i
    tty: true # equivalent to docekr run -t
```


How to rename a docker image:

```
docker tag CURRENT_IMAGE_NAME DESIRED_IMAGE_NAME
```


How to get extra information about an image:

```
IMAGE_ID=575878f109d7
sudo docker image inspect mongo # It's more humanreadable
sudo docker image inspect --format '{{json .}}' "$IMAGE_ID" | jq -r '. | {Id: .Id, Digest: .Digest, RepoDigests: .RepoDigests, Labels: .Config.Labels}'
```


How to get extra information about a container

```
docker inspect b5c2c4484e15 
You can grep anything that you want.
docker inspect b5c2c4484e15 | grep IPAdress
```

How to  solve pull issue in Iranian servers:
```
https://github.com/freedomofdevelopers/fod
# Note: sudo -i will disturb its ability
```

How to run Portainer:
```
sudo docker run -d -p 9045:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer:/data portainer/portainer
```

Why we should name our volumes in docker-compose:
```
volumes:
  db-data:
  pgadmin-data:

# Naming your volumes can help you with identifying and removing them in case of need.
```

How to enable buildkit in docker:
```
nano /etc/docekr/daemon.json
{ "features": { "buildkit": true } }
restart docker.daemon
# or
sudo DOCKER_BUILDKIT=1 COMPOSE_DOCKER_CLI_BUILD=1 docker-compose up --build
sudo DOCKER_BUILDKIT=1 COMPOSE_DOCKER_CLI_BUILD=1 docker build .
```

key or address-based  volumes:
```
volumes:
      - ./data:/data/db
This kind of volume binds a specific physical space on the host device to the one on the container

volumes:
      - data:/data/db
This is a key-based volume. You are binding a key to physical space on the container. Using this solely will result in an error because the key is not defined.
To solve the error you should define the key volume as a volume of the docker-compose file.
```

How to set volumes for nginx:
```
volumes:
   - ./nginx:/etc/nginx/conf.d
   - ./log/nginx:/var/log/nginx
```

what is --ulimit:
```
It limits the number of open files in a system.
$ limit -a >> shows you the number of allowed open files in your os
The same can be set for containers. Containers can't exceed the host's limitations in the number of open files. 
```

How to change input parameters of a dockerfile using system variables:
```
...
environments:
  -  Monitoring=${switch}
...
At run time: 
$ switch=On docker-compose up --build 
```

How to force docker-compose to build a specific container
```
sudo docker-compose up --build container-name
# ex:
sudo docker-compose up --build nginx-monitor
```

## How to change docker images' root-dir. 
Caution: Change in this directory may cause of a massive image and container loss
```
sudo systemctl stop docker.service
sudo systemctl stop docker.socket
sudo nano /lib/systemd/system/docker.service
# change following line:
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
# to:
ExecStart=/usr/bin/dockerd -g /home/ai/projects/docker-images  -H fd:// --containerd=/run/containerd/containerd.sock
# check
ps aux | grep -i docker | grep -v grep
# References: https://linuxconfig.org/how-to-move-docker-s-default-var-lib-docker-to-another-directory-on-ubuntu-debian-linux
```

How to restart:
```
sudo systemctl restart docker.socket docker.service
```

How to run a docker as a root user
```
sudo docker run -it --rm -u0 fluent/fluentd:v1.14-debian bash
# -u0
It's equivalent to: USER root inside docekrfiles
```

how to force delete an image or a container:
```
sudo docker rm -f container-id
sudo docker rmi -f image-id
```

how to restart a container using docker-compose:
```
docker-compose restart fluentd
```

Volumes in docker-composes:
```
volumes:
  myapp:
# This volume will be created at time of running in case it does not already exist.
# in this case the driver is empty and by default will set to "default"
```

```
volumes:
  myapp:
    external: true
# this volume must have been created before running docker-compose, like bellow
docker volume create myapp
```

To see the history of an image:
```
docker history --no-trunc IMAGE_NAME
```

How to check a dockerfile is ok or a linter for dockerfiles:
```
sudo docker run --rm -i hadolint/hadolint < Dockerfile
```

How to physically save a docker-image:
```
docker save IMAGE_NAME | bzip2 > imagename.bz2
```

Error WARNING: Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'NewConnectionError('<pip._vendor.urllib3.connection.HTTPSConnection object at 0x7f57cbb648b0>: Failed to establish a new connection: [Errno -3] Temporary failure in name resolution')': /simple/torch/
```
Disconnect VPN and restart your internet connection!
```

How to pass a bash variable(environment variable) to docker-compose:
```
# first export the variables in bash
export MINIO_ROOT_USER=<your-secrete-user-name>
export MINIO_ROOT_PASSWORD=<your-secrete-password>
# use in docker-compose
environment:
      - MINIO_ROOT_USER=${MINIO_ROOT_USER:-minio12345}
      - MINIO_ROOT_PASSWORD=${MINIO_ROOT_PASSWORD:-minio12345}
After `:` you can pass default values[It's a bash command]
```

## How to enable BuildKit in docker
```commandline
DOCKER_BUILDKIT=1 docker build .
```

## How to enable BuildKit in docker-compose
```commandline
COMPOSE_DOCKER_CLI_BUILD=1 docker-compose build
COMPOSE_DOCKER_CLI_BUILD=1 docker-compose up --build
# or 
COMPOSE_DOCKER_CLI_BUILD=1 DOCKER_BUILDKIT=1 docker-compose build
```

**NOTE:** Install `buildx` using:
```commandline
docekr install buildx
```
## How prune the following:
  - all stopped containers
  - all networks not used by at least one container
  - all images without at least one container associated to them
  - all build cache
```
docker system prune -a
```

## How to list containers running in by a docker-compose
```commandline
docker-compose ps
```

## How to exec to a container running by a docker-compose
```commandline
docker-compose exec <service-name> bash/sh
```

## Why choosing container raises error while replica is chosen:
Because there are more than one container, and each of them cannot have the same container_name! 