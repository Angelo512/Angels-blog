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

