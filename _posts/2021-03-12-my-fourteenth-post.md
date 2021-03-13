---
Layout: post
title: "Bash Basics 2: Bash Pipes"
date: 2021-03-12 12:00:00
categories: cl bash terminal
---

## **Bash Basics 2: Bash Pipes**

<br>

This blog post is a continuation of the previous blog post going over more bash basics. Here I will go over the power of bash piping. The use of the bash pipe allows a user to streamline a set of commands to achieve a specified and unique output. The pipe character is this one: \|. Here are a few examples of how the pipe command: 

<br>

---

**Example 1**

In this example, we will be redirecting the output of the ls -l command and then filter that output using the grep command to only show files in the current directory that are .txt files. 

``` bash
$ ls -l | grep "\.txt$"
```

<br>

---

**Example 2**

In this example, we will be printing out the contents of a file and then counting the amount of lines in that file 

``` bash
$ cat example1.txt | wc -l
```

<br>

