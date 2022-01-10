---
title: "Docker Introduction for Beginners"
date: 2022-01-10T16:41:55+05:30
draft: false
---


# What is Docker?
 [Docker](https://www.docker.com/) is an open platform that uses OS level virtualization to deliver software in packages called **containers**.
### What is a container?

- A way to package application with all the necessary dependencies and configuration.
- A portable artifact which can easily be shared and moved around.
- Using containers makes software development and deployment more efficient.

We can compare Docker containers with real world shipping containers. Just like shipping containers are used to package goods in them to easily send them wherever we want, Docker containers do the same job for software.
![Shipping containers](https://cdn.hashnode.com/res/hashnode/image/upload/v1628141634430/88k7NZVrK.jpeg)
### But where do Docker containers live?
Docker containers need a repository they can be hosted on. This repository can be :
- A company's private repository only accessible to authorized personals.
- Public repository for Docker container images called  [DockerHub](https://hub.docker.com/).
- Our own public or private container repository.

[DockerHub](https://hub.docker.com/) is the most popular source for getting Docker images. We can easily find official images for many popular technologies like [Ubuntu](https://hub.docker.com/_/ubuntu), [MongoDB](https://hub.docker.com/_/mongo), [Nginx](https://hub.docker.com/_/nginx), [Node](https://hub.docker.com/_/node) and countless others.
![DockerHub](https://cdn.hashnode.com/res/hashnode/image/upload/v1628142846823/y9tmZoe2c.png)
### How containers improved application development process?
To answer this question, let us see what were the difficulties before containerization existed and then compare it with the new ***container*** way.
#### Before containers :
- Each teammate had to install all the dependencies manually on their system to setup development environment.
- This installation process can be different on different Operating Systems.
- Many steps were involved in just setting up the environment which increases the chance of something going wrong.

#### After containers :
- No services are needed to be installed on each teammate's Operating System.
- Each container is its own isolated environment with all the dependencies packaged in it.
- Dependencies are packaged with all the needed configuration.
- We only need to run one command to start the container and we are ready to go.
- We can run two different versions of the same application at the same time (if required).

### How containers improved application deployment process?
#### Before containers :
- Folks needed to have configuration on the server.
- Dependency version conflicts may happen.
- There could be misunderstanding between Development and Operations team (due to textual guide for deployment)

#### After containers :
- Development and Operations team work together to package the application in a container.
- No environmental configuration is needed on the Server **except Docker runtime**.


# What is a Container? (technically)
- A container can be seen as multiple layers of Images.
- At the base of these layers, we generally have a [Linux](https://www.linux.org/) base image which should be small in size to keep the container small (which is one of the benefits of using containers). Due to this very reason, usually [Alpine](https://alpinelinux.org/) is used as preferred Linux distribution.
- On top of the layer structure, we have our application image, let's say [MongoDB](https://www.mongodb.com/).
![Container](https://cdn.hashnode.com/res/hashnode/image/upload/v1628151811731/g9NiqFKGk.jpeg)

### Docker Image and Docker Container
It is easy to get confused between Images and Containers, especially when we are beginners. So, let's just quickly see what they are
#### Docker Image
- **The actual package**, The application packaged with configuration, dependencies, etc is known as Image.
- Image is the artifact, we can move around, share with other people or put on Container repositories such as [DockerHub](https://hub.docker.com/).
- We can see Image as **non running state**.

#### Docker Container
- Container is a running environment for Image.
- Each running container has a port bound to it which is used to talk to application running inside it.
- Each container has an application image, a virtual file system and environment configs.
- We can see Containers as the **running state**.

# Docker Containers and Virtual Machines
- Any operating system is composed of a **Kernel** and **Application layer**. Kernel is the core layer of any OS and facilitates interactions between hardware and software components.
- Both Docker and VM are virtualization tools.
- The difference is Docker virtualizes on the Application layer, whereas a VM virtualizes at kernel level, thus, providing a complete Operating system environment.
![Virtualization](https://cdn.hashnode.com/res/hashnode/image/upload/v1628163131163/93G1XIwed.jpeg)

### Advantages of Containers over Virtual machines :
- *Size* -> Docker images are much smaller in size.
- *Speed* -> Docker containers run faster and start much faster.
- *Compatibility* -> Docker containers can run on any host OS.

*Note* that it is not about Containers "or" VMs. Both the technologies have their importance and are used as per the requirements.

# Installing Docker
Docker engine is available for all 3 major OS, [Windows](https://docs.docker.com/docker-for-windows/install/), [Mac](https://docs.docker.com/docker-for-mac/install/) and [Linux based on your distribution](https://docs.docker.com/engine/install/). Refer [official documentation](https://docs.docker.com/) for step by step guides.

**Note** that *containers are generally made for Linux and can't run on Windows systems directly. We will need [WSL(Windows subsystem for Linux)](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to work with Docker.*

**Note** that *the GUI tool, Docker Desktop is only available for Windows and Mac platform. On Linux, we can only use Docker through the CLI.*

# Most used Docker commands
### docker pull

```
$ docker pull <image name>
```
is used to pull (download) the image from container repository ([DockerHub](https://hub.docker.com/) in our case) to our local machine. For our example, we are going to [DockerHub](https://hub.docker.com/), search "mongo", copy the pull command of the official Mongo image and run it in our terminal.
![docker pull mongo](https://cdn.hashnode.com/res/hashnode/image/upload/v1628165794409/-HKj37cJzb.jpeg)

```
anubhav@anubhav:~$ docker pull mongo
Using default tag: latest
latest: Pulling from library/mongo
16ec32c2132b: Pull complete 
6335cf672677: Pull complete 
cbc70ccc8ebe: Pull complete 
0d1a3c6bd417: Pull complete 
960f3b9b27d3: Pull complete 
aff995a136b4: Pull complete 
4249be7550a8: Pull complete 
4da411c5a406: Pull complete 
4b9c6ac629be: Pull complete 
377bc7e5ccfa: Pull complete 
Digest: sha256:f04183826e91223d4f65399abfc2cb6f17d708b20d28566b4a4974755839622d
Status: Downloaded newer image for mongo:latest
docker.io/library/mongo:latest
anubhav@anubhav:~$ 
``` 
**Note** that if we don't mention the version of image, ```docker pull``` will pull the latest version available. If we need a specific version (let's say 4.4.8) of the image we will have to mention it like ```$ docker pull mongo:4.4.8```.

### docker images
```
$ docker images
```
is used to list all the existing images on our local machine along with their tag (version), image ID and size.
```
anubhav@anubhav:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
mongo         latest    49f9af59c1e4   15 hours ago   682MB
hello-world   latest    d1165f221234   5 months ago   13.3kB
anubhav@anubhav:~$
```
As we can see, we have two images present on our local machine, ```mongo``` and ```hello-world```.

### docker run
```
$ docker run <image name>
```
is used to start a new container from an image. If docker fails to find the image locally, ```docker run``` will automatically pull the image from [DockerHub](https://hub.docker.com/) and run it.
```
anubhav@anubhav:~$ docker run -d mongo
c7ecdb8c355830bad706ec23db667300bdb83b7e4d483b28a44c40c20fc22fe0
anubhav@anubhav:~$
```
**Note** that we have used ```-d``` attribute with ```docker run```. ```-d``` simply means "detach mode". If we don't use ```-d```, we will get live logs in our terminal.

#### But how will we use this running container?

Just starting the container with ```$ docker run``` is useless as we won't be able to access it if we don't bind the container's port and our host's port.
```
$ docker run -p<host port>:<container port>
```
is used to bind a specific port from host machine to a specific port of the container.

```
anubhav@anubhav:~$ docker run -d -p6000:6396 mongo
65549aea7da3ce583ebbcb392df30854964f471434ff3a522a83c845ac65ec68
anubhav@anubhav:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                                  NAMES
65549aea7da3   mongo     "docker-entrypoint.s…"   2 minutes ago    Up 27 seconds   27017/tcp, 0.0.0.0:6000->6396/tcp, :::6000->6396/tcp   pensive_noyce
c7ecdb8c3558   mongo     "docker-entrypoint.s…"   50 minutes ago   Up 6 seconds    27017/tcp                                              xenodochial_volhard
anubhav@anubhav:~$
```

**Note** the ```PORTS``` of our new container ```0.0.0.0:6000->6396/tcp, :::6000->6396/tcp``` shows that ```port 6000``` of host machine is now bounded to ```port 6396``` of container environment.

### docker ps
```
$ docker ps
```
is used to list all the containers currently running on our local machine along with information like container ID, image name, ports being used by the container and container's name.

**Note** that we can add ```-a``` attribute to ```docker ps``` to list all the containers(stopped or running) on our local machine.
```
anubhav@anubhav:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS       NAMES
c7ecdb8c3558   mongo     "docker-entrypoint.s…"   9 seconds ago   Up 9 seconds   27017/tcp   xenodochial_volhard
anubhav@anubhav:~$ docker ps -a
CONTAINER ID   IMAGE         COMMAND                  CREATED             STATUS                         PORTS       NAMES
c7ecdb8c3558   mongo         "docker-entrypoint.s…"   8 minutes ago       Up 8 minutes                   27017/tcp   xenodochial_volhard
7731539fe844   mongo         "docker-entrypoint.s…"   8 minutes ago       Exited (0) 8 minutes ago                   naughty_hodgkin
ffb68c57ae84   hello-world   "/hello"                 About an hour ago   Exited (0) About an hour ago               nostalgic_buck
e5eec66d2aae   hello-world   "/hello"                 About an hour ago   Exited (0) About an hour ago               relaxed_bouman
anubhav@anubhav:~$ 
```
As we can see, ```docker ps``` listed ```mongo``` as it is the only container currently running but ```docker ps -a``` listed two ```mongo``` and two ```hello-world``` containers which are all the containers present on our machine.

### docker stop
```
$ docker stop <container ID>
//OR
$ docker stop <container name>
```
is used to stop a running container.
```
anubhav@anubhav:~$ docker stop xenodochial_volhard
xenodochial_volhard
anubhav@anubhav:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
anubhav@anubhav:~$
```
As we can see, the ```mongo``` container is stopped and thus ```docker ps``` shows us no containers running.

**Note** that when a container is created, it gets a random name by default. If we wish, we can name the containers ourselves too at the time of creating them. I personally prefer using ```container name``` over ```container ID``` as it is easy to remember and faster to type in the command.

### docker start
```
$ docker start <container ID>
//OR
$ docker start <container name>
```
is used to start a stopped container.
```
anubhav@anubhav:~$ docker start xenodochial_volhard
xenodochial_volhard
anubhav@anubhav:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS         PORTS       NAMES
c7ecdb8c3558   mongo     "docker-entrypoint.s…"   32 minutes ago   Up 3 seconds   27017/tcp   xenodochial_volhard
anubhav@anubhav:~$
```

# Debugging Containers
Debugging in Docker is mainly done using two commands

### docker logs
```
$ docker logs <container ID or name>
```
is used to view the logs of a container.
```
anubhav@anubhav:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS          PORTS                                                  NAMES
65549aea7da3   mongo     "docker-entrypoint.s…"   15 minutes ago      Up 13 minutes   27017/tcp, 0.0.0.0:6000->6396/tcp, :::6000->6396/tcp   pensive_noyce
c7ecdb8c3558   mongo     "docker-entrypoint.s…"   About an hour ago   Up 13 minutes   27017/tcp                                              xenodochial_volhard
anubhav@anubhav:~$ docker logs 65549aea7da3
{"t":{"$date":"2021-08-05T13:35:56.516+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"thread1","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"}
{"t":{"$date":"2021-08-05T13:35:56.516+00:00"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"thread1","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":13},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":13},"outgoing":{"minWireVersion":0,"maxWireVersion":13},"isInternalClient":true}}}
.
.
.
.
{"t":{"$date":"2021-08-05T13:51:59.592+00:00"},"s":"I",  "c":"STORAGE",  "id":22430,   "ctx":"Checkpointer","msg":"WiredTiger message","attr":{"message":"[1628171519:592926][1:0x7f5c3d197700], WT_SESSION.checkpoint: [WT_VERB_CHECKPOINT_PROGRESS] saving checkpoint snapshot min: 17, snapshot max: 17 snapshot count: 0, oldest timestamp: (0, 0) , meta checkpoint timestamp: (0, 0)"}}
anubhav@anubhav:~$ 
```

### docker exec
```
$ docker exec -it <container ID or name> /bin/bash
```
is used to access the terminal of running container environment.

```-it``` attribute simply means "interactive", so that we get an interactive terminal.
```/bin/bash``` is used to access the bash of running container.
```
anubhav@anubhav:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS          PORTS                                                  NAMES
65549aea7da3   mongo     "docker-entrypoint.s…"   22 minutes ago      Up 20 minutes   27017/tcp, 0.0.0.0:6000->6396/tcp, :::6000->6396/tcp   pensive_noyce
c7ecdb8c3558   mongo     "docker-entrypoint.s…"   About an hour ago   Up 20 minutes   27017/tcp                                              xenodochial_volhard
anubhav@anubhav:~$ docker exec -it 65549aea7da3 /bin/bash
root@65549aea7da3:/# ls
bin   data  docker-entrypoint-initdb.d  home        lib    lib64   media  opt   root  sbin  sys  usr
boot  dev   etc                         js-yaml.js  lib32  libx32  mnt    proc  run   srv   tmp  var
root@65549aea7da3:/#
```
As we can see, we have got access to container```65549aea7da3```'s terminal as a ```root``` user.


# Thank you so much for reading 💖
This is my first blog ever. Hope you liked it.
Any feedback is highly appreciated :)

If you liked my work, share it with your friends

Feel free to ping me on socials
