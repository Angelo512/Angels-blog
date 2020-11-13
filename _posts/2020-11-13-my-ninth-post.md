---
Layout: post
title: "Ansible and AWS"
date: 2020-11-13 7:45:00
categories: ansible aws
---

## **Ansible and AWS EC2 Server Management**

<br>

In my previous post, I had given a short introduction of ansible and its powerful server management. In that post I used ansible to manage a ubuntu server running in docker and on my localhost. So for this post, I am going to run an ansible file against a running aws ec2 instance. 

<br>

**Step 1: Create A EC2 Intance In AWS**
1. So first you will need to sign into your personal aws account or your aws educate account 
2. Next you will need to traverse to the ec2 service from the service list page 
3. From there you will need to launch a new instance (for this example, pick a ubuntu ami like 20.01 or 18.04)
4. Make sure to add a ssh and a http security group! 
5. Attach or create a new .pem file as you will need this when you want to ssh into the ec2 instance. Make sure to chmod 0400 file as well.  
6. Once you have finished creating the ec2 instance, click on the connect button, and go to the ssh client tab 
7. At the very bottom, there should be something like: 

``` bash
$ ssh -i "[privatekeyfilename].pem" ubuntu@ec2-xx-xxx-xx-xxx.compute-1.amazonaws.com
``` 

8. Copy that file and run it inside the directory where the .pem file is located
9. Hit yes and you should be logged into your ec2 instance of either ubuntu 20.01 or 18.04 

<br>

**Step 2: Update The EC2 Instance**
Run this command: 

``` bash 
$ apt get update 
```
This update installs the latest version of python which is necessary for ansible to work its magic. 

<br>

**Step 3: Ansible And The Ansible Files**
So now we will create the .yml and .ini files that are necessary for ansible to work its magic on our instance. 

However, if you dont have ansible installed on your local machine, you will need to install it first. 
If your local machine is a Mac, then you will need to use the Homebrew to install it.
If your local machine is using Linux, then simply install it using apt.

For Mac users: 
``` bash
$ brew install ansible
```

For Linux users: 
``` bash 
$ apt install -y ansible
```
<br>

Alright so now onto the ansible files (perhaps create a ansible directory to store these files for efficiency): 

**YAML File**

Lets save this file as ec2-ansible.yml

So this is the .yml file that we will use in this example: 

``` yaml
---
- hosts: my_servers

  tasks:
    - name: Installing Nano text editor 
      become: true
      apt: name=nano state=present

    - name: Installing Apache
      become: true
      apt: name=apache2 state=present

    - name: Start apache2 service
      become: true 
      service:
        name: apache2
        state: started

    - name: Installing Snake :)
      become: true
      apt: name=nsnake state=present
```
So essentially we are installing both nano and apache2 

And then we will start the apache2 service if it had not already been started on install

And then, just for fun, we are installing the original snake game :)

<br>

**_However, notice something...._**

**_YES, the host field has the value: ec2_instance..._**

**_But what is that?_**

**Good Question! On to the next part**

<br>

**INI File**

So to start off this file is important as it lists the IP addresses of the servers you wish to connect to and manage 

You WIIL NEED to name the .ini file as hosts.ini

They could be arranged like this: 

[my_servers]

_insert 1st ip address here_

_insert 2nd ip address here_

_insert 3rd ip address here_

So for the .ini file you will create you will add a tag and name it whatever you want and then copy and paste the IPv4 address of your ec2 instance. Which should be located in the details tab.

**NOTE: Make sure that the name you gave is the same that will be on the .yml or else it will not work!**
> So lets say in the .ini you have:
>
> [my_servers]
> _ip address_
>
> then in the .yml file, in the host field you put: my_servers 

<br>

**Step 4: Run Ansible With The Newly Created Files**

To do this be in the same directory where both the .yml and .ini file are located. 

Make sure ssh is enabled on your ec2 instance. 

And run the following command: 

``` bash
$ ansible-playbook -i hosts.ini ec2-ansible.yml -u ubuntu --key-file /Location/of/file/privatekeyfile.pem
```
You should get this kind of input: 

``` bash
PLAY [my_servers] ***********************************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************************
ok: [IP address]

TASK [Installing Nano text editor] ********************************************************************************************************
ok: [IP address]

TASK [Installing Apache] ******************************************************************************************************************
changed: [IP address]

TASK [Start apache2 service] **************************************************************************************************************
ok: [IP address]

TASK [Installing Snake :)] ****************************************************************************************************************
changed: [IP address]

PLAY RECAP ********************************************************************************************************************************
IP address              : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

Alright so now you just have to ssh into your ec2 instance to check on everything you just did:
1. _install nano_
2. _install apache2_
3. _start apache2_
4. _install snake_

Once you've ssh'd into your ec2 instance you will notice that apache2 has been installed and that it currently running. If you had added the http security group to your ec2 instance, you could go on a web browser and hit search on your public IPv4 address or public IPv4 DNS  provided in the details tab of your ec2 instance.

You can stop the apache2 service if want

Now for the most important part...

Lets play **SNAKE**
``` bash
$ nsnake
```

``` bash
┌─eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee┐
│__    _  _______  __    _  _______  ___   _  _______  ┌Main Menu─uuuuuuuuuuuu┐│
│|  |  | ||       ||  |  | ||   _   ||   | | ||       |│Arcade Mode           ││
│|   |_| ||  _____||   |_| ||  |_|  ||   |_| ||    ___|│Level Select          ││
│|       || |_____ |       ||       ||      _||   |___ │Game Settings         ││
│|  _    ||_____  ||  _    ||       ||     |_ |    ___|│GUI Options           ││
│| | |   | _____| || | |   ||   _   ||    _  ||   |___ │Controls              ││
│|_|  |__||_______||_|  |__||__| |__||___| |_||_______|│Help                  ││
│                       o   o  ooo  oo                 │Quit                  ││
│    o   o              @   o  ooo  oo                 │                      ││
│    o   o o               oo  ooo  o@                 │                      ││
│    o   @ o     o         o@  o@o  oo           o    o│                      ││
│    o     o     @         o   o @  oo           o    o│                      ││
│    o     o               o   @ o  oo           o    o│                      ││
│    o     o               o     o  oo           o    o│                      ││
│    o     o               @     o  @o           o    o│                      ││
│ o  o     o                     o   o           o    o│                      ││
│ @  @     o        o            o   o           o    o│                      ││
│   o      o        o            o   @           o    o│                      ││
│   o      o        o  o         o               o    @│                      ││
│   o      o        o  o     o   o               o  o  │                      ││
│   o      o      o o  o     o   @o              o  o  │                      ││
│   o      @  o   o @  o  o  o    o      o       o  @  └─ttttttttttttttttttttt┘│          
```
Awesome :)

So all in all, ansible is an amazing tool to use when installing and managing your servers. This allows you to make any type of changes to the server with little work. Also if you wanted to do this to multiple aws ec2 instances, you could do all at the same time by simply adding the ip addresses of other ec2 instances. 

Very cool!





