---
Layout: post
title: "The NetCat Command"
date: 2020-11-20 19:00:00
categories: docker ubuntu netcat
---

## **Netcat: The TCP/IP Swiss Army Knife**

<br>

Today, I want to take a step back from ansible and focus on an important networking tool found on all Linux distros, netcat. As the title of post states, NetCat is essentially that swiss army knife of TCP/IP communication. 

According to it's very own man page, netcat "is a simple unix utility which reads and writes data across network connections, using TCP or UDP protocol. It is designed to be a reliable "back-end" tool that can be used directly or easily driven by other programs and scripts."

So in general this tool is a very cool way to connect machines via their ip addresses. And there are alot of cool things you can do with it!

So I will provide some examples of netcat's functionalities using our favourite VM tool: Docker. 

**Docker Setup**

1. First things first, create two docker containers (lets name them A and B) both running ubuntu 18.04 

2. Make sure you update and upgrade them both 

``` bash 
$ apt-get update && apt-get -y upgrade
$ yes | unminimize
```
3. Next run this command on both containers and record their respective IP address

``` bash
$ hostname -I
```
4. Now we are ready for netcat 


**Netcat Commands**

So first things first lets make a connection between container A and B and demonstrate a basic messaging system: 
1. On container A, execute the following command: 

``` bash
$ nc -nlvp 4444
```

2. On container B, execute the following command: 

``` bash 
$ nc -nv IP.Address.of.A 4444
```

3. Now start typing away! 

Note that in this example container A is acting as the listening server and container B is therefore the client. This can be easily pointed out by the -l flag in the nc command executed on container A.

Alright One more cool feature of netcat is that you can transfer files between machines.

1. On container A, lets create a .txt file with some basic content
``` bash
$ echo "Hello!" > payload.txt
```

2. On container B, create a file to recieve the content from container A
``` bash
$ nc -nlvp 4444 > fromA.txt
```

3. Now back on container A, lets send in our created file 
``` bash
$ nc -nv ip.address.of.B 4444 < payload.txt
```

4. Once the transfer is done, next ctrl+c on container A 

5. Finally, on container B, if you use the ls command then the file fromA.txt should now be there including the "Hello!" text

NetCat is pretty cool!


