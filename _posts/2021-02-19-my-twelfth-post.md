---
Layout: post
title: "Introduction to Terraform"
date: 2021-02-19 12:00:00
categories: AWS EC2 Terraform 
---

## **Introduction Into Terraform**

<br>

In a sense, Terraform and Ansible (discussed in an earlier blog) as they are both sofwares which focus on IT automation. However, Terraform in particular focuses on automating the building and servicing of IT infrastructure through efficient automation.

<br>

The standard syntax for terraform is as follows: 

``` terraform
    <BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
        # Block body
        <IDENTIFIER> = <EXPRESSION> # Argument
    }
```