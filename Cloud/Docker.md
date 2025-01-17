# What is Docker?

Docker is containerization platform that packages applications and their dependencies together in isolated environment called containers to make sure that applications run consistently, regardless of underlying environment.

# Why do we need Docker

The most essential need of Docker is to remove "It works on my machine" problem. It can make your development easier and streamline the process of deployment and scaling the application.

Lets say you have an application built in your local machine, for your colleague to get started with the application, has to perform various steps like installing all the required software and dependencies, and then setting up code and then running it. More steps means the chances of doing something wrong is also high.

How do you make sure you have the same versions as the other developers on your team? Or your CI/CD system? Or what's used in production?

How do you ensure the version of Python (or Node or the database) your app needs isn't affected by what's already on your machine? How do you manage potential conflicts?

Docker removes all these problems. You can create a container or containers using docker compose which will install everything with just one command. 

This way our application will not depend on the platform and runs independently and safely.

# Important Components

## Container

They are the closed environment  that allows you to package you application with all the necessary dependencies and configuration to run your application.

**Containers are also defined as "isolated runnable instance of an image"**

They are portable, easy to share and move around

### Commands

#### Running a container

```bash
docker run -it <image-name>
```

docker run = docker pull + docker start

it follows the form:

```bash
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```

[options] = Lets you configure options for container. Below are the important options.
* -d (detached mode) = run it as a background process, otherwise it will be stuck at cmd
* --name = Give name to the container

[commands and arguments] = Specify commands and Args for container to run when it starts up.
* -it = interactive
* sh = shell

#### see list of all containers
```bash
docker ps -a
```
 ps = processes
-a = all, to show all running and stopped containers
#### stop a container
```bash
docker stop <container-id>
```
you get the container id from above command 

#### Start a container
```bash
docker start <container-id>
```

#### Delete a stopped container
```bash
docker delete <container-id>
```

#### Delete all stopped containers
```bash
docker container prune
```



When you run a docker container run command, it first checks if the specified image is in the local machines and will create a container from it, otherwise it check in the registry, pulls the image to local and then run it. This is why you should delete the image from the local machine if you are frequently making any changes.

## Image

Image is like a read only blue print or template with instructions for creating a container. It is a package that includes all of the files, binaries and libraries and configuration, basically everything you need to create and run a container.


### Commands

#### Pull image to local machine from registry
```bash
docker pull <image-name>
```

#### Build image with a tag
```bash
docker build -t <image-path> .
```
"." here represents current directory. That means this command needs to run where Dockerfile is present

#### Publishing image
```bash
docker push <repository-path>
```

#### Delete all images
```bash
docker images prune -a
```

### images are layered

Container images are composed of layers and each layers once created are immutable. The main benefit of layers is reusability between these images of these layers.

For example: imaging you created a container with python base image. Now if you want to create another container with python base image, then docker will reuse this layers instead again pulling and creating the python base from scratch. It saves 


## Difference between image and container

* Container is a running env for image. Has virtual file system and has ports

## Dockerfile

IT is a text based document which can be of json and yaml format that's used to create a container image. Usually it is a yaml file (industry standards). It provides instructions to the image builder on the commands to run, files to copy and more.

### Common instructions

* FROM (image) - this specifies the base image of the container
* WORKDIR (path) - the path in the image where files will be copied and commands will be executed
* COPY (host-path) (image-path) -  copy files from host and put them into the container image
* RUN (command) - tell builder to run the specified command
* ENV (name) (value) - set an environment variable for the container
* EXPOSE (port-number) - indicates a port the image would like to expose (this only for documentation, original port will be in docker run command)
* CMD ["command", "arg1"] - default command a container using this image will run

## Publishing ports

Containers provide isolated processes for each component of your application. Each component - a react frontend, a python API, a database - run in its own sandbox env, completely isolated from everything else on host machine. This isolation is great for security and managing dependencies but it also means that you can't access them directly.

To access the application running inside the container we have to use ports. We have add port forwarding while running the containers.

```bash
docker run -d -p HOST_PORT:CONTAINER_PORT <image-name>
```

Consider it like "Forwarding traffic from host port to the container port."
## Container Registry

We need a place to store our containers, like we need github to store our code. Container registry is a special container storage that allows you to store containers.

There are many registries like DockerHub, ECR etc

## Volumes

The containers storage is ephemeral in nature. Meaning, when the container is deleted all the data stored in the container is also deleted. 

Sometimes, we need to persist the data. This means, we need a mechanism which is independent of the container life cycle, this is where volumes come into picture.

Volumes are the storage mechanism that provides the ability to persist the data beyond the life cycle of a container. Using it we can attach a directory in the host computer to a directory inside the container. These both directories will now be connected with each other and anything that you store inside the directory of the container will be stored also on the mounted directory of the host machine.

#### Create volumes
```bash
docker volume create log-data
```

#### Run container with a volume attached
```bash
docker run -d -p 80:80 -v log-data:/storage1 <image-name>
```
Attaches a volume called log-data to the container. If the volume log-data does not exist then docker will create it for us.

#### See list of all volumes
```bash
docker volume ls
```


### Bind mount

Docker offers two primary ways of persistent storage: 1) Volumes, 2) Bind Mount

Bind mount means attaching a specific directory of the host machine to the container to share the storage between host machine and docker container. This is really useful when you want to share a set of files like a env file which has passwords with the container, since adding it in the image might be a security risk. 

### Volume vs Bind mount

The main difference between Volume and Bind mount. Bind mounts does have any name, they are just directories in the host machine which we are mounting in the container Where as volumes are have name but we do not have any idea where the files are stored. The whole storage is handled by docker for us, which makes it a good option for file storage persistence.

Bind mount
```bash
docker run -d -v .:/storage1 <image-name>
```

mount the current directory to the directory called storage1 in the container. We can also provide name of the volume instead of just current directory. Here instead of volume name you give a specific directory



