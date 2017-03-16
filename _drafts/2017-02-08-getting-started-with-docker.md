---
post_title: Getting started with Docker Basics 
author: Rahul Patil
post_date: Wed Feb  8 14:01:09 CET 2017
categories: [ docker, containers ]
layout: post
published: true
---

# Introduction 

In this tutorial we will learn following things:

   - What is Containers
   - Why Containers
   - Containers vs VM's
   - What is Docker
   - Docker component and architecture 
   - Docker Installation & Setup on CentOS 7
   - Docker basic commands  


# In Traditional way of virtualization  

As we used lot of VMs for dev testing or any R & D purpose or may be for different different VMs for applications, 
But actually we create VM then we install OS then we host our application in that OS, so its actually takes much resouces. 
in this scenario you will have to give 1G memory for VM OS then for application.  

But if you use containers then you will save resources and you will utilize for proper application use only. 

Take look at following diagram, it's shows the difference as mention above.. 

![VMvsContainer](http://windowsitpro.com/site-files/windowsitpro.com/files/uploads/2015/01/docker%20overview.jpg)

---

**Let's see some basics concept about Containers :** 

# What is Containers ?

  - Containers are similar to hardware virtualization like VMs but instead of partitioned the physical machines 
    containers isolate the process in single operating system. 
  - To do this docker leverages some features in underlying operating system kernel, to create multiple isolated userspace process. 
  - On top of this docker provide features like docker cli
  - Docker also provide imaging system. 


**Let's compare the containers with VM's, so that you will get more idea**

# Containers Vs. Virtual Machines

| VMs | Docker |
|---|---|
| Each VM runs its own Operating system | All containers share the same kernel of Host |
| Host OS can be different than guest OS | Host OS and container OS has to be same | 
| No such concept in VM | Containers stop when the command it is started with completes| 
| VM take few minutes to boot| Containers take few milli seconds to start |
| VM snapshots are hugh in size | Images are built incrementally on top of another like layers| 
| VMs are not version controlled, can't check diff in two VMs| Images can be diffed and can be version controlled using Dockerhub( like github) |
| In normal 4 GB laptop we can run 3-4 VMs| We can run many docker containers | 
| You can run only 1 VM using 1 VMDK file | Many docker containers can be started from one docker image| 


---
 
# Why Containers ?

Four key benefits of using containers 

  - Portable : Image can be ship, it's mutable, image has versions 
  - Flexible : You can create clean, reprodusable and moduler environment 
  - Fast     : Speed at start quickly containers, Caching layer of docker make faster build container 
  - Efficient : we can allocate exactly resource we want like cpu,memory, it does require full operating system. 

---

But where this containers fits in usecase ? hmm.. to understand this we need to know some concept, so lets see that 
  
# Microservices architecture.. 

> Previously companies were  building one single web application or any application, 
there will be Hugh downtime for any changes because it's one single application, so now days companies are using 
microservice approaches because smaller services can handle with separate teams and it can scale and manage individual by team. 

# Continaers are natural for microservices 

  - Simple to model: Dockerfile 
  - Any app, any languages
  - Image is the version 
  - Test & deploy same artifact 
  - stateless servers decrease change risk 
  
# Containers Providers
  - Docker ( We will learn this ) 
  - AWS ECS
  - LXD
  - LXC

---

Docker is supported by almot all the big players in the cloud computing market e.g.(Amazon, Azure, RackSpace , etc.), so we will focus on docker, lets start with basics:
 
# What is Docker?
> Docker is an open platform for developers and sysadmins to build, ship, and run distributed applications. Consisting of Docker Engine, a portable, lightweight runtime and packaging tool, and Docker Hub, a cloud service for sharing applications and automating workflows, Docker enables apps to be quickly assembled from components and eliminates the friction between development, QA, and production environments. As a result, IT can ship faster and run the same app, unchanged, on laptops, data center VMs, and any cloud.

# Docker Architecture

Docker uses a client-server architecture. The Docker client talks to the Docker daemon, 
which does the heavy lifting of building, running, and distributing your Docker containers.
The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. 
The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.

![Docker_Arch](https://docs.docker.com/engine/article-img/architecture.svg)

  - **Docker daemon ( Engine)** : The Docker daemon runs on a host machine. The user uses the Docker client to interact with the daemon. The Docker engine is the actual middle-ware that runs, monitors, orchestrate the containers
  
  - **Docker client** : in the form of the docker binary, is the primary user interface to Docker. It accepts commands and configuration flags from the user and communicates with a Docker daemon. One client can even communicate with multiple unrelated daemons.
  
  - **Docker Image**:  A Docker image is a read-only template with instructions for creating a Docker container. For example, an image might contain an Ubuntu operating system with Apache web server and your web application installed. You can build or update images from scratch or download and use images created by others. An image may be based on, or may extend, one or more other images. A docker image is described in text file called a Dockerfile, which has a simple, well-defined syntax.
  
  - **Docker containers** : A Docker container is a runnable instance of a Docker image. You can run, start, stop, move, or delete a container using Docker API or CLI commands. When you run a container, you can provide configuration metadata such as networking information or environment variables. Each container is an isolated and secure application platform, but can be given access to resources running in a different host or container, as well as persistent storage or databases. 
  
  - **Docker registries** :  A docker registry is a library of images. A registry can be public or private, and can be on the same server as the Docker daemon or Docker client, or on a totally separate server. take look at public registry Docker hub at https://hub.docker.com/explore/
 
**Docker filesystem**

Docker uses Union File System ( with Storage driver AUFS for Ubuntu and driver devicemapper for RHEL/CentOS ) 

UnionFS used because:

  - it's Avoid duplicating a complete set of files each time you run an image as a new container
  - it's isolate changes to a container filesystem in its own layer, allowing for that same container to be restarted from a known content (since the layer with the changes will have been dismissed when the container is removed)

Read more about filesystem, and [How does docker image work](https://docs.docker.com/engine/understanding-docker/#/how-does-a-docker-image-work)

---

# Installation 

### Prerequisites

**Docker must be installed on 64 bit OS with kernel more than 3.10. The kernel must support an appropriate storage driver.**

### Installation on CentOS 7

**1. Add Official docker repo**

```shell
cat << EOF > /etc/yum.repos.d/docker.repo
[Docker]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/7
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
```

**2. Install docker-engine**

```shell
yum install -y docker-engine
```

Note: if docker is already install, make sure to remove older version using `yum remove docker container-selinux docker-common docker-client`

**3. Start service and add in startup**

```shell
systemctl restart docker.service
chkconfig --level 35 docker on
# check docker info using 
docker info
```

**4. Testing Docker**

```shell
docker run hello-world
```

**Output will be like**

```shell
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
78445dd45222: Pull complete 
Digest: sha256:c5515758d4c5e1e838e9cd307f6c6a0d620b5e07e6f927b07d05f6d12a1ac8d7
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
```

In Next tutorial we will see, some usefull handson on docker :)

Feel free to comment or email if you have any question/suggessions  
