---
Layout: post
title: "How To Add Aliases In Bash On Your Mac"
date: 2020-12-09 12:00:00
categories: bash mac terminal aliases 
---

## **Speed Up Your Workflow!** How To Add Aliases On Your Mac Machine

<br>

As you probably know or you do not know already but an alias is a user defined change to an existing command or the creation of a new command (somewhat in the realm of automation). In fact, using aliases you can automate and mainstream which and the amount of commands you execute in your daily workflow. You can even make commands better than their default versions, allow me to explain...

<br>

**The Setup**

1. First things first, open terminal on your mac, and execute this command: 
``` bash
$ cd ~ 
```
2. Now we are going to find an important (and hidden) file within your home directory which is the **<ins>.bash_profile</ins>** file 
``` bash
$ ls -la | grep bash 
``` 
3. Once you list the file, next simply just nano the file
``` bash
$ nano .bash_profile 
```
4. Now we just add our custom commands 

<br>

**Adding our aliases** 

So you know how a command has their own default use which can be altered by its options? Well it can get somewhat tiresome just typing them in constantly and maybe you might forget the ones you use. Well here we can edit the commands so that they match our preferences. For example, in order to see the .bash_profile we need to use the -a option as it reveals all files even the hidden ones, the ones preceeded by a '.' in its file name. Well using the power of aliases we can make ls -a the default execution of the command ls. Like this: 

``` bash
alias ls = `ls -a`
```

Then just write out and save it.

**NOTE: This change only takes effect if you restart the terminal application**

Now if you were to execute the ls command it will perform the definition you gave it which is ls -a. 

<br>

This is just one very simple example of the amazing capabilities of aliases.