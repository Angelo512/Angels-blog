---
Layout: post
title: "Bash Basics 3: How to Rename and Move Directories"
date: 2021-04-16 12:00:00
categories: cl bash terminal
---

## **Bash Basics 3: Renaming and Moving Directories**

<br>

This blog post is part 3 of the Bash Basics Series. For today's lesson, I will go over how to rename and move directories within your bash terminal all through the command line.

<br>

---

**Renaming Your Directories**

So for this example, we are going to use this directory: _myfolder_ and renaming it _mynewfolder_. 
In order to do this we will need to use the `mv` command. The `mv` command, according to the bash man page: 

> In its first form, the mv utility renames the file named by the source operand to the destination path named by the target operand. This form is assumed when the last operand does not name an already existing directory.

> In its second form, mv moves each file named by a source operand to a destination file in the existing directory named by the directory operand.

So, in other words, this command will allow us to both rename and/or move our directories depending on the destination we give those files. 

Alright, lets get started, to rename a directory you need to traverse to the location of that directory and then type this command to rename this directory (for this example lets assume the directory is located within the home (~) directory): 

``` bash
mv ~/myfolder ~/mynewfolder
```

<br>

---

**Moving Your Directories**

So for this example, we will be using the same directory: _myfolder_.
In order to move this directory to a new location you will need to use the same `mv` command but we need to specify the new location/path of the directory. For this example we are moving _myfolder_ from our home directory (~) to root (/): 

``` bash
mv ~/myfolder /myfolder 
```

<br>

