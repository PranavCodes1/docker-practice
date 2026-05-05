docker is a platform that helps us build containers.

docker container- a single unit in which we package our application and all dependencies into a single unit.
properties of container-
1.Portable- we share a docker image so that we can share container with different devices.
2.lightweight in nature- it has very less overhead, simple to use, size is very less as compared to vm.


docker image- its an executable file which ahs instructions for building container.
so docker image is blueprint that can create multiple containers.

we share dockr image so that everyone in our team can create containers from it.

size of the image is very small, and container uses the resources of our machine, not docker image.

example command-

1. docker run -it ubuntu 
this command runs ubuntu in interactive mode that is we can use its terminal, inside a container.


DockerHub-
docker public images can be acessed from here.


Commands-

1.docker pull image-name = pulls image from dockerhub, if not available in local environment
ex- docker pull hello-world

2.docker images - shows us all the images that we have

tags are associated with images- tags are versions of image.
every image has a image id

2.docker run image-name
used to build container from docker image.
containers have their own unique id


DockerHub-
docker public images can be acessed from here.


Commands-

1.docker pull image-name = pulls image from dockerhub, if not available in local environment
ex- docker pull hello-world

2.docker images - shows us all the images that we have

tags are associated with images- tags are versions of image.
every image has a image id

2.docker run image-name
used to build container from docker image.
containers have their own unique id


DockerHub-
docker public images can be acessed from here.


Commands-

1.docker pull image-name = pulls image from dockerhub, if not available in local environment
ex- docker pull hello-world

2.docker images - shows us all the images that we have

tags are associated with images- tags are versions of image.
every image has a image id

2.docker run image-name
used to build container from docker image.
containers have their own unique id


DockerHub-
docker public images can be acessed from here.


Commands-

1.docker pull image-name = pulls image from dockerhub, if not available in local environment
ex- docker pull hello-world

2.docker images - shows us all the images that we have

tags are associated with images- tags are versions of image.
every image has a image id

2.docker run image-name
used to build container from docker image.
containers have their own unique id

3.docker run -it imagename
to run docker containers in interactive mode, interactive mode allows us to access the container terminal.

4. docker ps -a
-a means all containers
it shows all containers

5.docker ps 
shows running containers

6.docker start cont-name or cont-id
to restart existing container

7.docker stop cont-name or cont-id
to stop container

8.docker rmi image-name
removes/destroys an image

9.docker rm cont-name
removes container

10.docker pull image-name:version
to download specific version of an image
ex- docker pull mysql:8.0

11.docker run -d image-name
-d means detach mode, we can run any container in background

12.docker run --name cont-name -d iamge-name
we can give custom name to our container


Layers of docker images- every img is a collection of layers

container layer
layer 2- read only 
layer 1- read only
base layer- linux layer


Port binding-
all docker containers have a port that are by default binded

host machine ports and container ports are separate but we can bind them also.

command
docker run -phostport:containerport iamge-name
ex- docker run -p8080:3306 image-name

here host port is mapped to container port which is called as port binding.

host machine port can be binded with only one container port.


Troubleshoot Commands-
used for checking errors

1.docker logs cont-id
can access logs of specific container, which helps identifying root cause of problem

2.docker exec -it cont-id /bin/bash 
it allows to run additional commands to run on a running container, inside terminal of container.



DOCKER VS VM
docker uses machine host OS kernel and virtualizes application layer.

vm virtualizes both- host  os kernel as well as application layer.

this is the reason docker is lightweight in size and faster.

docker was initially built for linux based os.



Docker Network- used for interaction of containers with each other.

command-
1.docker network ls
to check all docker network

2.docker network create network-name
to create a docker network



DOCKER COMPOSE-

Docker compose is a tool for defining and running multi-container applications.

writing all commands in a sin gle file called .yaml.
so that we wil run containers from files instead of terminal.
these commands are in structured way.

in compose.yaml we write-
indetation is imp so use proper spacing.
version: docker compose version we want to use
services: services are the containers that we want to run
mongo:
ports: for port binding
environment: env variables

ex-
version: "3.8"
services:
	mongo:
	image: mongo
	ports:
	-27017:27017
	environment:
		MONGO_INITDB_ROOT_USERNAME:admin
		MONGO_INITDB_ROOT_PASSWORD:qwerty
	volumes:
	-host_dir:cont_dir
	
TO RUN THIS YAML FILES, WE USE DOCKER COMPOSE
Commands of docker compose-

1. docker compose -f fileName.yaml up -d
to create and run the containers defined in file.

2. docker compose -f fileName.yaml down
to delete the containers permanently

in yaml file we do not need to create docker network, it automatically creates a network.


JENKINS CONVERTS OUR APPLICATION INTO DOCKER IMAGE, SO THAT EVERYONE CAN BE ABLE TO ACCESS THE PARTICULAR IMAGE.

DOCKER FILE-
blueprint for building docker image and docker container.
DOCKER FILE has instructions how the application will be dockerized.


IMP docker file instructions-
FROM- we write base image, on which we will be creating our docker app, ex- FROM node.js
WORKDIR- Defining our working directory, its the path in the image where files will be copied and commands will be executed.
COPY- to copy files from host to image.
RUN- helps to execute instructions, ex- run pip install, there can be multiple run commands.
CMD- we can have only one cmd command,after setup of container, its a default command that will be used for running the container.
EXPOSE- expose port of any image.
ENV- environment variables are defined here.



TO CREATE A CONTAINER FROM DOCKER FILE-
COMMAND- docker build -t image-name:version .
here -t is tag
ex - docker build -t testapp:1.0 .

to run container- docker run testapp:1.0

Publsihing docker images on DOCKERHUB-

1.Create a new repository.

2. build docker image with rthe same name given to the repository
ex-docker build -t docker_practice/testapp

3.login in dockerhub from terminal,
command- docker login -u <username>


DOCKER VOLUMES-
Volumes are persistent data stores for containers, to prevent from data loss.
we define it by -v
ex - docker run -it -v /users/desktop/data:/test/data ubuntu

so volumes helps us to store data even after we stop or delete the container. so that it is stored in our desktop.


to get all volumes- docker volumes ls

to create custom volume- docker volume create VOL_NAME

to remove created vomulme- docker volume rm VOL_NAME


to attach these created volumes with running containers-

named volumes	-	
docker run -v vol_name:cont_dir

Anonymous volumes-
docker run -v MOUNT_PATH
Here mount path is container directory

Bind Mount-
docker run -v HOST_DIR:CONT_DIR


docker volume prune- to delete anonymous volumes that are not in use.
