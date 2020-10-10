---
Layout: post
title: "HELP! Where are the man pages on Ubuntu 18.04?! Here's An Easy Fix"
date: 2020-10-09 10:00:00
categories: Docker Ubuntu-18.04 Unminimize 
---

### **"So I Spun Up A New Docker Container Using Ubuntu 18.04 And It Says That The Command 'man' Does Not Exist! Help!"**
<br>

***"Hello there, Lets "triage" your problem..."***
<br>
<br>
<br>
Step 1: Spinning Up A New Container
>```bash
> $ docker run --rm -it ubuntu:18.04 bash
>```

> This here sets up a temporary container that will delete itself when you exit out of it. 

Step 2: Check the current version of the ubuntu version just to be sure 
>```bash
> $ cat /etc/issue
> Output: Ubuntu 18.04.5 LTS \n \l
>```

> Alright so everything looks fine so far 

Step 3: Man command on man just to test if man-db is installed 
>```bash
> $ man man
> Output: bash: man: command not found
>```

> Alright now I see the issue, here's what I think is happening...

Ubuntu Linux distros like 18.04 and 20.01 are maintained by their respective organizations in their own repos. 

Perhaps when you pull a new image from this repo, they have made changes to the image so that it includes the bare minimum of binaries. 

In order to restore all the content and packages that are necessary for a default Ubuntu Server system, you can run this script: 
>```bash
> $ unminimize | yes
>```

> The yes portion is to avoid the pesky question of yes or no to go foward with the various packages that are going to be installed. Note: this might take some time! 

So Lets run it, Step 4: Run the unminimize command
>```bash
> $ unminimize | yes
> This system has been minimized by removing packages and content that are
> not required on a system that users do not log into.
>
> This script restores content and packages that are found on a default
> Ubuntu server system in order to make this system more suitable for
> interactive use.
>
> Reinstallation of packages may fail due to changes to the system
> configuration, the presence of third-party packages, or for other
> reasons.
>
> This operation may take some time.
>
>
> Re-enabling installation of all documentation in dpkg...
> Updating package list and upgrading packages...
> Get:1 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]
> Get:2 http://archive.ubuntu.com/ubuntu bionic InRelease [242 kB]
> (blah blah blah)...
> $
>```

Step 5: The Results
>```bash
> $ man man
>```

> Now you ***SHOULD*** be directed to a man page for the man command :)
