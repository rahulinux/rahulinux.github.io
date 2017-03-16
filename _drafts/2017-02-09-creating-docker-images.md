---
layout: post
title: "Creating custom docker images"
date: Thu Feb  9 10:03:38 CET 2017
categories: docker
---

# Introduction 
In previous post we have learn about container technology, docker installation and docker useful commands, now we will learn how to build our own custom docker images. 


There are two options we have for building custom images in docker

  - **1. Docker commit** : rarely used 
  - **2. Dockerfile** : this is mostly used and recommended


## Docker commit 

Let say you have running container and you made some required changes and you want to create new image of this container. 

Usage:

```shell
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```


 


