---
layout: post
title: "Deep-understand-Bash"
date: 2013-07-24 22:55
comments: true
categories: 
---

### Bash and sh

*** Basic concepts ***

Bash is Bourne again shell, ```ls -l /bin/bash```,then ```ls -l /bin/sh```,
then you will find, ```/bin/sh -> bash```, ```sh``` equals to ```bash --posix```,
now in Ubuntu System you will find ```/bin/sh -> dash```, ```dash``` is different
with ```bash```, it's for script executing, not for interaction, it's fast but
less functions than ```bash```, and it comply with POSIX.

<!-- more -->

*** Specify an interpreter for script ***

You write a script, you may write ```#!/bin/bash``` in first line,
the you run ```chmod +x script```, then run it, it will use bash 
interpreter to run it, or write ```/bin/bash script``` to specify a 
interpreter and ```#!/bin/bash``` will be no use.

*** Differences ***

    

### Type of shell

Login shell, none-loginshell, interactive shell and non-interactive shell.


### Startup files of different type of shell

