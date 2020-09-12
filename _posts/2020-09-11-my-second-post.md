---
layout: post
title:  "Installing Apache on a Linux Ubuntu Machine"
date:   2020-09-11 17:30:00 
category: Ubuntu Apache
---

## **What is Apache?** 

As you know, the internet is simply the communication between two entities: the **<ins>client</ins>** and the **<ins>server</ins>**. To simplify, the client is just the web browser that is installed on a computer while the server is what serves these web browsers information aka web pages. 

Now **Apache** is service that can be installed on a linux distro, in this case lets try ubuntu, and it can be used to serve web pages that you make locally on your ubuntu machine. 

Luckily it is very simple to install apache on Ubuntu.

## **Installing Apache** 

First order of business, it is best practice to upgrade ubuntu first 
> ```bash
> $ apt-get upgrade 
> ```

Next, we just simply install apache
> ```bash
> $ apt-get install apache2 -y
> ```
(**NOTE:** We add the -y option so as to avoid any pesky yes or no questions )

After that we are done :) 
We have offically installed apache... Now how do we view it? 

So to view all the files that make up apache they primarily live in two places: 
* **/etc/apache2** - configuration files
    * Within this directory you find config files such as: 
        * apache2.conf  
        * conf-available  
        * conf-enabled  
        * envvars  
        * magic  
        * mods-available  
        * mods-enabled  
        * ports.conf  
        * sites-available  
        * sites-enabled
* **/var/www/html** - web pages
* **/var/logs/apache2** - logs for apache 

So to **<ins>start</ins>** apache you need to run the command: 
>```bash
> $ sudo service apache2 start
>```

To **<ins>stop</ins>** apache you need to run the command: 
>```bash
> $ sudo service apache2 stop
>```

And to view the **<ins>status</ins>** all you need to do is run the status command: 
>```bash
> $ sudo service apache2 status
>```

Finally, you can view the status of your server by viewing if it serving your webpages. 
All you would have to do is to open your browser on your ubuntu machine and type in the search bar:
* http://local.server.ip