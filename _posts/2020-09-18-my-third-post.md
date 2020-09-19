---
Layout: post
title: "How To Install A LAMP Stack"
date: 2020-09-18 17:30:00
categories: Linux Apache MySQL PHP
---

## **What Is A LAMP Stack?**

#### ***Linux, Apache, MySQL, and PHP***

As the above title reads, a LAMP stack is a combination of Linux(The OS), Apache(The Web Server), MySQL(The Database), and PHP(The Programming Language). 

> ***NOTE**: PHP can be dropped into languages like HTML to provide the "pulling-of-data" from a database.*

Together these software components can allow you to create web applications.

## **Installation of LAMP Stack**

> ***NOTE**: For this exercise, we will practice creating a LAMP stack inside a docker container.*

#### **PART 1: *Linux***

So the first part of creating a LAMP stack is to install Linux, in this case we will opt for the ubuntu flavor (v18.04 to be precise). Lets create a new container with ubuntu and map local port 8080 to port 80 inside the container: 
> ```bash
> $ docker run -it -p 8080:80 --name [NAME] ubuntu:18.04 bash
> ```
> *Replace [NAME] with whatever name you want*

Next we just have to update and upgrade so that we have all the necessary packages to proceed with LAMP installation and we should also install a text editor while we are at it: 

> ```bash
> $ apt-get update && apt-get update && apt-get install -y nano 
> ```

#### **PART 2: *Apache***

Now we will install the Apache Web Server:

> ```bash
> $ apt-get install apache2
> ```

Now check if it is successfully installed: 

> ```bash
> $ apache2 -v
> ```

In order to start the server and test if you need to start the service: 
> ```bash
> $ service apache2 start 
> ```

and type ***localhost:8080*** into your web browser. If an Apache2 Ubuntu Default Page pops up then it is working.

#### **PART 3: *MySQL***

Next, we install the our RDMS for the database portion of the web application:
> ```bash
> $ apt-get install -y mysql-client
> ```

Now to check if it installed successfully: 

> ```bash
> $ dpkg --get-selections | grep mysql
> ```

#### **PART 4: *PHP***

Finally, we install our programming language, PHP: 
> ```bash
> $ apt-get install -y php libapache2-mod-php php-mysql php7.2-cli php7.2-curl php7.2-gd php7.2-mbstring php7.2-mysql php7.2-xml php-xml
> ```

And then we check to see if php installed: 

> ```bash
> $ php -v
> ```


After this final step, you have finally created your very own LAMP stack. Yay! :^)






