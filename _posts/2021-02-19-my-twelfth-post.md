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

So lets go over the syntax according to the [terraform.io website](https://www.terraform.io/docs/language/index.html): 

**Blocks** - containers for other content and usually represent the configuration of some kind of object, like a resource. Blocks have a block type, can have zero or more labels, and have a body that contains any number of arguments and nested blocks. Most of Terraform's features are controlled by top-level blocks in a configuration file.

**Arguments** - assign a value to a name. They appear within blocks.

**Expressions** - represent a value, either literally or by referencing and combining other values. They appear as values for arguments, or within other expressions.