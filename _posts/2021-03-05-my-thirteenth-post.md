---
Layout: post
title: "Bash Basics 1: How to Redirect Input and Output"
date: 2021-03-05 12:00:00
categories: cl bash terminal
---

## **Bash Basics 1: How to Redirect Input and Output**

<br> 

Mastering the power of the command line and bash scripting is important for your future as an IT professional. In this blog post, I will go over an important skill to learn which is the power of redirection. Redirection, as the name suggests, is a Linux feature that allows you to change the standard input and output devices. As you know the stdin and stdout are is the keyboard and the screen but with redirection we can change that often for added utility/functionality. 

<br>

---

**Output Redirection (>)**

So a simple example of basic output redirection is writing to a file the output of a certain command, in this case, the output of the <ins>ls</ins> command written to a new file: 

``` bash
$ ls -a > file1
$ cat file1
```

---

<br>

**Input Redirection (<)**

Here is a simple exampe of input redirection: 

``` bash
$ wc -l < file1
$ 12 - This being the amount of lines within the file1 file
``` 