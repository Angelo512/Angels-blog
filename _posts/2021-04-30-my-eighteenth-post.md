---
Layout: post
title: "How to use Ansible to create AWS EC2 dynamic inventory file"
date: 2021-04-30 12:00:00
categories: bash ansible aws ec2
---

## **Ansible-AWS EC2 Dynamic Inventory**

<br>

**_Background: Ansible Host File_**

On a previous [blog post](https://angelo512.github.io/Angels-blog/aws/ansible/ec2/2021/04/09/my-fifthteen-post.html), I went over how to set up and use anisble on updating your ec2 infrastructure. Recall how I mentioned the need to create a host file, `hosts.ini`, which lists the public IPs of your EC2 instances? Well, one of the major flaws of that `hosts.ini` file is that you need to constantly change it to make way for new IP addresses or delete unused ones. In other words, it can be a hassle when your working in a changing environment. Therefore there is the option to use a dynamic list that grabs the IP addresses of EC2 instances that fall under user-specified ranges. Cool! Now lets go over on how to do it...


<br>


**_Setting Up Ansible On Your Admin Terminal_**

First things first, decide what should be your admin terminal. (Preferbly a bastion server that has connection to all your ec2 instances.)[https://angelo512.github.io/Angels-blog/bash/aws/ec2/bastion/2021/04/23/my-sevententh-post.html]

For this blog post lets assume we did this on a bastion server 

_On Your Bastion..._

Execute the following command, also make sure to hit enter and yes whenever prompted to do so: 
``` bash
$ sudo apt update
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update -y
$ sudo apt-get install ansible -y
$ ansible --version
$ sudo apt install python-pip
$ sudo pip install botocore
$ sudo pip install boto3
```
**Ansible.cfg**

Next, we need to edit the ansible.cfg file to include the necessary plugins so: 
``` bash
$ sudo nano /etc/ansible.cfg
```
Traverse to the `[inventory]` section and add the following under `[inventory]`:
``` bash
enable_plugins = aws_ec2, host_list, script, auto, yaml, ini, toml
```

**aws_ec2.yml**

Now we have to create our dynamic list modifier which will contain your `aws access key`, `aws secret key`, and your specified `region(s)` where your EC2 Instances are located:
``` bash
$ sudo nano ~/aws_ec2.yml
```

Your file should look something like this (**NOTE**: In this example our file is looking for ec2 instances with tags of the Key/Name type, you can do whatever you want but for this example I am filtering via the tags my ec2 instances have with them): 

``` yaml 
plugin: aws_ec2
aws_access_key: # Enter your aws access key
aws_secret_key: # Enter the secret acccess key of your aws
regions:
  - # Use Region of Resources
keyed_groups:
  - key: tags
    prefix: tags 
``` 

**Listing Your EC2 Instances**

Now the moment of truth! Traverse to the same directory as where your aws_ec2.yml file is located, make sure your bastion and your ec2 instances are all running, and it also wouldn't hurt if your bastion can also successfulle ssh into each ec2 instance (because why not :D ), and run this command: 

``` bash
$ ansible-inventory -i aws_ec2.yml --graph
```

And now you can see all your aws ec2 instances!