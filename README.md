# A Look Inside Some Concepts Of Container 
- By Lakshmi

<img src ="https://miro.medium.com/v2/resize:fit:720/format:webp/0*odPqaXggmqAIR3kS">


## TABLE OF CONTENTS

- [Introduction](#introduction)
- [Image Building](#image-building)
- - [Step-1](#step-1-create-a-dockerfile)
- - [Step-2](#step-2-convert-the-dockerfile-to-image)
- [Image Running](#image-running)
- - [Step-1](#step-1-run-docker-image-into-container)
- [Container Runtimes](#container-runtime)
- [Container Registry](#container-registry)
  


## Introduction

<img src ="https://enterprisersproject.com/sites/default/files/styles/large/public/images/CIO%20Containers%20Ecosystem.png?itok=oSrmsEqL">

In this document, we will learn some concepts of container.


## Image Building

### Step-1 Create a Dockerfile

<img src = "https://miro.medium.com/v2/resize:fit:600/format:webp/0*nX1z5vaygpdwyukK.jpeg">

Dockerfile is a text file with no extension that consists the sequential sets of multiple instructions in order to build up the image from it, and that image later on runs into the container for the particular applications to run smoothly.

#### Commands to run at the terminal
```bash
nano Dockerfile
```
- Dockerfile Example

```bash

# Use the official Ubuntu base image
FROM ubuntu:22.04

# Set the creator label
LABEL Creator="Lakshmi"

# Update package list and install Apache
RUN apt-get update \
    && apt-get install -y apache2 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV APACHE_RUN_USER=www-data
ENV APACHE_RUN_GROUP=www-data
ENV APACHE_LOG_DIR=/var/log/apache2

# Expose port 80
EXPOSE 80

# Start Apache in the foreground
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]

```


### Step-2 Convert the Dockerfile to Image

<img src ="https://i.sstatic.net/jc2IW.jpg">

An image is a static file that consists of codes, instructions, and tools which were executed to make a container on a system for a programmer to containerise its programme, and that container can run any device in terms of its configurations. Either you can generate it from the self-written Dockerfile or you can use another person's uploaded images that are already present at the Registry (i.e., DockerHub).

#### Command to run at the terminal
```bash
docker build -t img_apache .
```
- To verify image formation run the below command.

```bash
docker images 

#Output
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
img_apache    latest    f00e5deb752b   8 seconds ago   186MB
alpine        latest    91ef0af61f39   2 months ago    7.8MB
hello-world   latest    d2c94e258dcb   18 months ago   13.3kB

```

## Image Running

### Step-1 Run Docker image into Container 

<img src ="https://geekflare.com/cdn-cgi/image/width=697,height=270,fit=crop,quality=90,format=auto,onerror=redirect,metadata=none/wp-content/uploads/2019/07/dockerfile-697x270.png">

<img src ="https://blog.stephane-robert.info/_astro/conteneurs-docker.B7C9bP3q_2j5j5z.webp">

A container is like a package that consists of all dependencies(like codes, tools, and settings) that are needed by an app or website to run on each device(i.e., on Android or IOS or Windows phones & laptops/desktops with Windows/Mac/Linux OS)

#### Command to run at the terminal
```bash

docker run -itd --name cont_apache -p 8080:80 img_apache

#Output Container Id
c9c127235e2401fe4871551447579c95d1d0b4cc96fa5e3e8d2fc63e16dda6a5

```
- To verify Conatiner formation run the below command.

```bash
docker ps -a

#Output we get
CONTAINER ID   IMAGE        COMMAND                  CREATED         STATUS                     PORTS     NAMES
c9c127235e24   img_apache   "/usr/sbin/apache2 -…"   8 seconds ago   Exited (1) 8 seconds ago             cont_apache

```

## Run the container application on the web browser

```bash
http://localhost:8080
```

![Screenshot from 2024-11-13 18-05-21](https://github.com/user-attachments/assets/336c43c4-8ca3-447d-8bf6-aa98691b26e8)


## Container Runtime

<img src ="https://panzhongxian.cn/images/demystifying-containers-part-ii-container-runtimes/cncf-landscape-container-runtime.png">

<img src ="https://www.ianlewis.org/assets/images/771/runtime-architecture.png">

Container runtime is part of the containerization tool, that is responsible for starting, running, stopping & managing the container So, that the container runs smoothly in any environment. 

There are two types of Container Runtime: -
- Low Level
A low-level container runtime is the basic tool that directly manages the containers. It is responsible for starting and stopping containers, like creating and managing the container’s file system, networking, and resources. Examples: - Youki, Containerd

- High Level
A high-level container runtime builds on top of low-level runtimes and also Works with it so, that provides extra tools which make it easier to work with containers. It is responsible for building, and pushing images to registries, managing multi-container setups, and more. Examples: - Docker, Docker, Amazon ECS


## Container Registry

<img src ="https://learn.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction/media/docker-containers-images-registries/taxonomy-of-docker-terms-and-concepts.png">

The Container Registry is the place where the images are stored. We can either store the images on the local registry or can also save them in the public registry by pushing images to be used by others as well. We can also pull the images from other public registries as well.
