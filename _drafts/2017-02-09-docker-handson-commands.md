---
post_title: HandsOn on docker commands 
author: Rahul Patil
post_date: Wed Feb  9 13:01:09 CET 2017
categories: [ docker,docker-cli, containers ]
layout: post
published: true
---

# Introduction 

In the previous tutorial, we have learn about docker and containers and Installation of docker. 
now we will see how to play with container because handling containers is the sole purpose of all these infrastructure. 

## 1. RUN command 

```shell
docker run hello-world
```

**Whats just happend?** 

Basically once you run above command, it's do following things:

  - Check "hello-world" image is exists or not locally, that's why you see first msg "Unable to find.." in first ran
  - Pullimage from docker hub if not exists in local
  - Create container from downloaded image with some random name 
  - Start the container in forground mode ( all output on TTY ) from downloaded image 
  - Once process is finished then it will stop the container, in our case it was just print hello-world message.

If you want to run container in background then you can simply pass `-d` flag to run command as below:

```shell
docker run -d centos "/bin/bash"
```
It will run container in detached mode. 

Another command for interactive mode:

```shell
docker run -i -t centos "/bin/bash"
```

Run command has many option, you can check `man docker-run` for more info, some basic overview as below:

The run options control the image’s runtime behavior in a container. These settings affect:

  - detached or foreground running
  - container identification and name
  - network settings and host name
  - runtime constraints on CPU and memory
  - privileges and LXC configuration


---

## 2. Create command

Create command only create container with settings you provided, it does not start container. 

Example:

To create :

```shell
docker create --name test-cn -i -t centos "/bin/bash"
```

Output:

```shell
d63f927cf1c9cc7899389dfddb52fd104b4f2ed7a211e11cf994ea7a644fdd7d
```
The output you see, it's a container ID, every container has uniq id, we have provided name (test-cn) to container, if you do not provided name then you can use container id, which is output of above command 

To start :

```shell
docker start -a -i test-cn
```

OR 

```shell
docker start -a -i d63f927cf1c
```

---

## 3. Start, Stop and Restart command 

To change the container state, you can use thise command like our init script. 

When you fire stop command, docker actually sends signal -15 ( SIGTERM), to the process. The SIGTERM signal requests the process to terminate itself gracefully. once signal sends,
docker will wait for some timeout... if its does not stop, then after timeout, docker will send SIGTERM signal ( -9 ) to kill the process forcefully. 

Usage:

```
docker stop | start| restart [OPTIONS] CONTAINER [CONTAINER...]

[Options]
-t, --time=10      Seconds to wait for stop before killing it

[Container]    
Control the container either by Name or ID
``` 

---

## 4. Exec command 

Now let say you have runing container, and you want to run some commands in runing container, in this case you can use `exec` command: 

```shell
docker exec -t test-cn bash -c "cat /etc/hosts"
```

```shell
docker exec -it test-cn bash
```

This will create new bash session in the running container. 

---

## 5. cp command 

Copy data from/to running container

Example:

```shell
docker cp test-cn:/etc/hosts test-cn-hosts-file
```

This will copy hosts file from test-cn container to local path with name test-cn-hosts-file

Usage:

```shell
docker cp [OPTIONS] CONTAINER:PATH LOCALPATH
docker cp [OPTIONS] LOCALPATH|- CONTAINER:PATH
```
---

## 6. attach command 

This commands brings a container to the foreground. The container must be running to be attached.

Usage:

```shell
docker attach [OPTIONS] CONTAINER
```

Example:

```shell
docker attach test-cn
```

Once you run exit command or after attaching container you kill process inside container, it will go to stop mode. 

---

## 7. Inspect command 

It will gives you all container system information like network,os,driver etc... in json format. 

Example:

```shell
docker inspect test-cn
```

---

## 8. rm command 

This command is used to delete any container either by name or ID. Put Make sure that the container is stopped before you remove it.

```shell
docker rm CONTAINER-ID
```

---

## 9. ps command 

Shows the current running containers on the system and with -a flag list all containers that has been created 

To check running containers

```shell
docker ps 
```

for checking all containers

```shell
docker ps -a 
```


---

## 10. Search and pull image

If you want to search any ready image let say for java then you can simply use search and pull 

To search all java images:

```shell
docker search java
```

To pull on java image:

```shell
docker pull java
```

---

## 11. Docker save and load image and list images

Lets say you have created your custom image, now you want to export in file and copy to another server then you can simply use this option, its just for portable version of docker images.

Usage:

```shell
docker save -o test-cn.tar test-cn 
docker load --input test-cn 
``` 

To list downloaded images

```shell
docker images
```

## Mix command 

To stop all container in one single command 

```shell
docker stop 'docker ps -aq'
```

I hope this is useful for you, feel free to email/comment if any quires.

In next tutorial we will learn about building docker images. 


