---
Layout: post
title: "What are Dockerfiles And How Do You Use Them"
date: 2020-10-02 10:00:00
categories: Docker Dockerfile
---

### **What Is A Dockerfile**

Whenever you spin up a new docker container, it is recquired that you pull an image of an OS of your choosing which in turn will be the OS that your docker container is running. 

The images that you pull from the docker image library are pre-created and have their own commands, binaries, directories, etc files, etc.

However, Docker grants users the ability to create their own docker images. With this functionality we can set up new containers using our user-specific configurations off the get go. 

For example, lets say I want to make an image that uses a specific ubuntu version coupled with a couple of common set-up commands such as apt-get update and apt-get upgrade. We can build this image using a Dockerfile so that we do not have to type those commands when we first boot up that docker container. 

This functionality allows for greater automation when creating docker containers. 

So lets do an example run shall we...


### **How To Create And Build Your Own Dockerfile**

**Step 1: Create Dockerfile**
- So we need to create a file with the exact name: "Dockerfile"
- Lets say we create this in a directory named: "DockerFiles"
>```bash
> $ mkdir DockerFiles .
> $ touch Dockerfile
> $ nano Dockerfile
>```

**Step 2: Write Inside That Dockerfile**
- Now we will write inside this Dockerfile 
- Take particular note of the formatting as it is important

>```bash
> # grabbing ubuntu image 
> FROM ubuntu:18.04
> 
> RUN apt-get update && apt-get upgrade -y
> RUN yes | unminimize
> RUN apt-get install -y sudo
>```

- Save the Dockerfile when you are done

> NOTE: the FROM and the RUN commands,
> We are grabbing ubuntu version 18.04, 
> And we are running a total of 4 commands: update, upgrade, unminimize, and install 

**Step 3: Build An Image Using That Dockerfile**
- Make sure docker is already running and that you are currently inside the directory where you created the Dockerfile

>```bash
> $ docker build -t myimage .
>```

- It will now build that image and given that there are no errors on your dockerfile code and no issues with the docker daemon service then it should build without a problem

> NOTE: -t option is to provide a name for this image,
> myimage is the name we are giving the newly built image 

**Step 4: Check Your Docker Images**
- Easy way to check: just run this command 

>```bash
> $ docker images -a
>```

> -a option stands for all

**Step 5: Test Your Image**
- Now we can just test your image by using an temporary or expendable docker container 

>```bash
> $ docker run -rm -it myimage bash
>```

- So with this command you should boot into a new docker container that is using your custom-made docker image 


Now we have officially created your own custom docker image using the powerfull functionality of Dockerfile. :)