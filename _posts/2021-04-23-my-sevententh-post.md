---
Layout: post 
title: "How To Create A Bastion Host/Jumpbox EC2 Instance On AWS"
date: 2021-04-23 12:00:00
categories: bash aws ec2 bastion
---

## **AWS EC2 Bastion Host/Jumpbox**

<br>

For today's post, we will take a look at how we can create an ec2 bastion server that will allow us connection to your private ec2 servers. First off lets go over why we would need a bastion host or jumpbox to begin with, security.

<br>

---
<br>

**_Security_**

When given the choice to host a website or a web application on a AWS EC2 instance, one must consider the traffic it can receive. It can be alot of traffic or little but nevertheless serving the website on the internet means anyone can have access to your site. With this availability comes with the possibility of malicious activity. Some individuals can attempt to hack into your website and obtain root/admin access of your website without permission. Therefore you choose to close as much access to it as possible. But at the same time, you still need to have the ability to login to your private ec2 instance to perform regular updates and changes. Therefore you have a "middle man" of sorts. This is known as bastion host. The idea of a bastion host is that it is an ec2 instance with only ssh access from known ip addresses (so you and your admin team) and this bastion is the only ec2 instance with ssh access to your private ec2 instance: 

<p align="center">
admin ----ssh----> bastion ----ssh----> private server
</p>

---

**_Bastion-Host And Private-Server Creation_**

So for practice on how this bastion-host to private server scenario would work, spin up two ec2 instances: 

1. Bastion-Host
    * Choose all the **free options** 
    * Choose the **default VPC**
    * Choose to enable a **public IP address**
    * Create a **Security Group** of **SSH from My IP**
        * This allows only you to ssh into this bastion instance
    * Create a **new .pem key** and name it: **bastion_host_key**
2. Private Server
    * Choose all the **free options**
    * Choose the **default VPC**
    * **DONT** choose to enable a **public IP address**. Choose **disable**
        > Notice that there will be only a private ip address and no public address
    * Create a **Security Group** of **SSH from Anywhere**
        > "From anywhere?? Isnt this a private server?" We'll get there...
    * Create a **new .pem key** and name it: **private_server_key**

---

**_Editing The Private-Server Security Groups_**

After creating your ec2 instances, copy the public and private ip addresses of your _bastion-host_ and add them to the ssh rule you gave to the _private-server_. Make it so that only those 2 ip addresses are the only ones to have ssh access to the _private-server_. Save that rule.


---

**_Logging Into Your Bastion-Host_**

So just traverse to the same directory where your **bastion_host_key**, open a terminal window, and ssh into it using the following command: 

``` bash
$ ssh -i "bastion_host_key.pem" ubuntu@public-ip-address
```

If you can login then it means you can now login into your _private-server_ now.
But first, copy the _private-server_ key into your _bastion-host_ in a new terminal window.

``` bash
$ scp -i "bastion_host_key.pem" /local/location/of/private_server_key.pem ubuntu@ip-address-of-bastion-host:/home/ubuntu/
```

---

**_Logging Into Your Private-Server_**

So now to ssh into your _private-server_ through your _bastion-host_. From within your _bastion-host_, traverse to where you copied over the private key of the _private-server_ (so essentially /home/ubuntu) and type this command: 

``` bash
$ ssh -i "private_server_key.pem" ubuntu@private-ip-address-of-private-server
```

And now you should be logged into your _private-server_! And you can confirm you are inside your _private-server_ by typing the `ifconfig` command.