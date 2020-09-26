---
Layout: post
title: "How to SSH and SCP Into Your AWS EC2 Instance"
date: 2020-09-25 13:00:00
categories: Amazon-AWS EC2-Instance PEM-Keys SSH SCP
---

### **What is SSH and SCP?**

#### <ins>***SSH And SCP***</ins>

SSH, according to its man page, is is a program for logging into a remote machine and for executing commands on a remote machine 

SCP (which stands for secure copy), according to its man page, copies files between hosts on a network. However, it uses SSH for data transer and uses the same authentication and security as SSH. It will also ask for passwords for authentication if needed. 

### **SSH'ing Into Your EC2 Instance**

Here is a small list of what you need to successfully SSH into your EC2 Instance: 

- An EC2 Instance (let's say it is running Ubuntu)
- An SSH client of your choice 
- The private key file that you received when creating this specific instance 
- The public DNS of your instance 
- The username of your instance (if you are using ubuntu then it would be: ubuntu@...)

First things first, you have to change the permissions of your pem file to 400,

So navigate to the directory where that key was downloaded on your public key,

Next run this command: 
>```bash
> $ chmod 400 private-key-file.pem
>```

Now you would locate your instance's public DNS and username (in this case, if we are using ubuntu then the username is ubuntu).

That string would something like this for example: 
> ubuntu@XX-XX-XXX-XXX.compute.amazonaws.com

Finally you would run this command to finally ssh into your EC2 Instance of Ubuntu Linux:
>```bash
> $ ssh -i private-key-file.pem ubuntu@XX-XX-XXX-XXX.compute.amazonaws.com 
>```

And you will prompted with a "Are you sure you want to continue connecting?”,

Answer Yes,

And hopefull you will be in! :)

### **SCP Files Between Your Local Machine And Ubuntu-Linux Instance**

To secure copy files from your computer to your instance is very similar to the process of SSH'ing into your instance.

To successfull copy files you need the following: 
- Private Key that your instance created 
- The full path to your local file 
- your instance username and public DNS

Here is the command: 
>```bash
> $ scp -i private-key-file.pem ~/Desktop/HelloWorld.txt ubuntu@XX-XX-XXX-XXX.compute.amazonaws.com:~/Desktop/
>```

That seems pretty straightfoward but what if I wanted to do the reverse? Easy: 
>```bash
> $ scp -i private-key-file.pem ubuntu@XX-XX-XXX-XXX.compute.amazonaws.com:~/Desktop/GoodbyeWorld.txt ~/Desktop/
>```




