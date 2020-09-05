---
layout: post
title:  "Creating A New Docker Container"
date:   2020-09-04 15:03:00 
categories: jekyll Docker CIT480
permalink: /docker/
---
## **What is Docker?**

What does **Docker** and VirtualMachine Softwares, for example: **Oracle VitualBox**, have in common? They are both **<ins>virtualization softwares</ins>**. 

However if you have never used or even heard of **Docker**, it is totally fine, I was in the same boat as you. I was introduced to **Docker** very early during college and it was my first introduction into the power of virtualization. However, the manner of how **Docker** deals with the task of virtualizing software allows it, in my own opinion, to be <ins>**lighter**</ins> and <ins>**faster**</ins> than its contemporaries. 

---

## **How Does Docker Work?**

As said previously, **Docker** is a virtualization software however what makes it different is that it allows the user to run programs as applications on your host machine totally through the Command-Line. Let me explain further: 

* Using Docker and the Command-Line shell of your choice
* You use the docker command to pull an image
    * These images are similar to the ISOs offered by software distributors  
* Then using the docker command, you can create a container which runs the docker image you just pulled
    * These containers are lightweight and capable of executing a package of software 
    * Also they have everything needed to run the application from the code to the libraries to the settings

So in short, with only a few commands, you have a small VM of a software of your choice within your host machine that is completely independent from it. But if you do want communication **Docker** containers allow you to easily move or copy files to and from your host machine and your container. So in short, **Docker** is:

* Lightweight
* Fast 
* Powerfull

---

## **Creating a Docker Container**

What you will need: 
* **Docker** 
* Terminal/CLI Client Application

Where do I go to install **Docker**?
> [**Docker Install**](https://docs.docker.com/engine/install/)

Once you have **Docker** installed, a good way to check if it actually did install is to go into your command line application and type the following: 
> ```bash
> $ docker --version
> ```

or

> ```bash
> $ docker -v
> ```

Next, you are going to pull a new docker image from the docker server:
* In this example, we will pulling ubuntu linux version 18.04 

> ```bash
> $ docker pull ubuntu:18.04
> ```

* This command will pull the latest build version of Ubuntu 18.04

Then, we will actually create our new container using that ubuntu image we just pulled:

* Replace NAME with whatever name you want for the container

> ```bash
> $ docker container run -it --name NAME ubuntu:18.04 bash
> $ exit
> ```

If everything happened accordingly without any issues, if you were to execute the following command:

> ```bash
> $ docker container ls -a
> ```

* The output of the above command then the docker container you have just created will be listed there 

Alright so you successfully created your first ubuntu docker container! Now what? Well, you set it up. First you have to restart the container and login to it.

> ```bash
> $ docker start NAME
> $ docker exec -it NAME bash
> ```

Finally you upgrade and update your container: 

> ```bash
> $ apt-get update && apt-get install -y sudo
> ```

Now once you have finished that step, you have officially created and initialized your first docker container running an ubuntu image. Hooray!





