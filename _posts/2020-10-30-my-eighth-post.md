---
Layout: post 
title: "Introduction To Ansible"
date: 2020-10-30 10:30:00
category: ansible docker 
---

## **What is Ansible?** 

_**In short, IT Automation**_

<br>

Ansible is a python-based IT automation tool. This tool is very useful as it can help with the continuous configuration and deployment of common systems. It runs in an agent-less manner and uses SSH to connect with hosts. So how does it work in the real world? Well it is very similar to a dockerfile for example but it can be applied to many different systems, on different services, at the _**SAME TIME**_. So let's show an example of using ansible to configure a ubuntu server docker container (of the 18.04 flavor). 

<br>

## **Ansible And Docker**

First things first, we need to install ansible in our docker container. So just spin up a new container using ubuntu: 18.04: 

``` bash
$ docker container run -it -p 8080:80 --name testing_ansible ubuntu:18.04 /bin/bash
$ apt-get update && apt-get upgrade -y
$ apt-get install -y ansible
$ mkdir -p /home/ansible ; cd /home/ansible
```

**OR**

If you recall the dockerfile post, just add ansible to your dockerfile, create the docker image, and use that image when creating your docker container

``` bash
# grabbing ubuntu image 
FROM ubuntu:18.04
 
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y ansible
RUN mkdir -p /home/ansible
WORKDIR /home/ansible 
```

```bash
$ dockerfile -t ansible_image .
$ docker container run -it -p 8080:80 --name testing_ansible ansible_image /bin/bash
```

> NOTE: I add an ansible directory into the dockerfile so we have somewhere to work from /
> You dont need to do this but it is more organized this way

Now once inside your docker container you need to run this command on the .yml which contains the configuration details for you system (run this inside the same directory ): 

``` bash
$ ansible-playbook our_file.yml
```

So lets look an example yaml file, which will look very familiar if you pay attention to previous blog posts:

``` yaml
---
- hosts: 127.0.0.1
  connection: localhost

  tasks:
    - name: Installing Required Packages 
      apt:
        name:
          - nano
          - git
          - curl 
          - zip
        state: present


    - name: Installing Apache
      apt: name=apache2 state=present


    - name: Start apache2 service 
      service:
        name: apache2
        state: started


    - name: Installing MySQL
      apt: name=mysql-client state=present


    - name: Install PHP
      apt:
        name:
          - php
          - libapache2-mod-php
          - php-mysql
          - php7.2-cli
          - php7.2-curl
          - php7.2-gd
          - php7.2-mbstring
          - php7.2-mysql
          - php7.2-xml
          - php-xml
        state: present

```
So essentially this yaml file installs a lamp stack, well technically an amp stack since ubuntu is a linux distro but you get the idea. So lets break down each _task_...

**Hosts**

So we are running this command inside our docker container and since our docker container is already on localhost we need to point this yaml file to localhost.

**Task 1: Installing Required Packages**

So essentially tasks are the assignments to do within the server so in other configuration instructions. Each task is divided by a name in which each name does its own assignment or task. Name is where you add the name of the package you want to install and state...well think of state like if statement. If said package is not present within your OS, then install said package into the OS. This results in name=blah state=present. Here this is the format if you have multiple packages to download in one name task 

**Task 2: Installing Apache**
So pretty straightfoward, installing apache if it is not there 

**Task 3: Start Apache Service**
Here we are starting the apache2 service if and only if it has NOT started already hence the "state: started". Notice the service word where it would be the apt word. These are known as ansible modules. Each module has its on functions and arguments, as you can see here: [Ansible Module Documentation](https://docs.ansible.com/ansible/2.3/apt_module.html) 
<br>
And the other tasks are more or less the same.

<br>
So Thats About It!
<br>
If you have a stable connection and your syntax is not incorrect (remember this is python-based so SPACING MATTERS) then you good to go!


