---
Layout: post
title: "Using Ansible Playbook on AWS "
date: 2021-04-09 12:00:00
categories: AWS Ansible EC2 
---

## **Using Anisble Playbook on AWS**

<br>

On a previous [blog post](https://angelo512.github.io/Angels-blog/ansible%20docker/2020/10/30/my-eighth-post.html), I went over an introduction on what is [Ansible](https://docs.ansible.com/ansible/latest/index.html) and how to use an Ansible Playbook specifically in that blog post we executed it on a docker ubuntu 18.04 container.

<br>

This time we will executing an ansible playbook on an EC2 instance on AWS. More or less it is the same process as executing the playbook on the docker instance but with some added steps: 
1. Creating the EC2 Instance
2. Adding SSH access to anyone (or your own IP)
3. Creating a .pem key and changing the permissions (chmod 0400 .../.pem)
4. Updating your ec2 instance 

<br>

---

**Prepping The EC2 Instance**

After launching your instance, open your terminal on your mac or linux machine and enter the following command: 

``` bash
ssh -i "NAMEOFFILE.pem" ubuntu@IP-ADDRESS-OF-INSTANCE
```

Once logged into your instance, enter the following command: 

``` bash
$ sudo apt update 
```

Afterwards check if python is installed: 

``` bash
$ python3 --version
```

<br>

---

**Sample Ansible PlayBook**

For our sample ansible playbook, we will do something relatively simple which is installing a web server in this case apache2. 

Our sample ansible playbook, we'll name it _ansible-playbook.yml_: 

``` yaml
---
- hosts: web_server

  tasks:
    - name: Installing Apache
      apt: name=apache2 state=present

    - name: Start apache2 service 
      service:
        name: apache2
        state: started
``` 

Create a new file name _hosts.ini_ which will contain the IP Address of your EC2 Instance: 

[web_server]
XXX.XXX.XXX.XXX

Next,

Enter the following command in a new terminal: 

``` bash
$ ansible-playbook -i hosts.ini ansible-playbook.yml -u ubuntu --key-file .../NAMEOFFILE.pem
```

<br>

If there are now errors, then your EC2 instance will be installed with apache2 and will serve the default apache web page when you enter the IP Address in your browser. 



