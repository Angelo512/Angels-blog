---
Layout: post 
title: "How To Copy Files Between Your Host OS And Your Docker Container"
date: 2020-10-16 10:30:00
category: Docker Copy Files
---

## **How Does The Docker CP Commnand Even Work?**

_**Let's allow docker and our terminal answer this question for us**_

>```bash
> $ docker --help | grep cp
> cp          Copy files/folders between a container and the local filesystem
> $ docker cp --help
>
> Usage:  docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
>	      docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
>
> Copy files/folders between a container and the local filesystem
>
> Use '-' as the source to read a tar archive from stdin
> and extract it to a directory destination in a container.
> Use '-' as the destination to stream a tar archive of a
> container source to stdout.
>
> Options:
>   -a, --archive       Archive mode (copy all uid/gid information)
>   -L, --follow-link   Always follow symbol link in SRC_PATH
> $ 
>```

<br>

### **Alright Lets Break Down The Above Output**

**_What does this command do: docker cp [OPTIONS] CONTAINER:SRC_PATH  DEST_PATH\|\-_**

So to put it simply, this command does the following action: 

container-name:location-of-file-in-container ----> location-to-be-on-host-machine

**_What does this command do: docker cp [OPTIONS] SRC_PATH\|\-  CONTAINER:DEST_PATH_**

And not suprisingly, this command does the opposite of the former: 

location-of-file-on-host-machine ----> container-name:locaiton-to-be-on-container

**_What does the '-' do and the available options do_**

For the sake of this post, I won't go into detail now perhaps in a future post. 

<br>

### **Example of docker cp**

_**Copy file from container to host machine**_

>```bash
> $ docker start my-container
> my-container
> $ docker cp my-container:/Hello_World.txt /
> $ cd /
> $ ls | grep Hello_World.txt
> Hello_World.txt
>```

_**Copy file from host machine to container**_

>```bash
> $ docker start my-container
> my-container
> $ docker cp /Hello_World.txt my-container:/
> $ docker exec -it my-container bash
> $ cd /
> $ ls | grep Hello_World.txt
> Hello_World.txt
>```
