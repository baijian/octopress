---
layout: post
title: "grub-rescue-in-linux"
date: 2013-03-16 16:42
comments: true
categories: 
---

Grub rescue prompt to rescue your linux
---

## What is grub?

Of course you should know it if you have ever used linux operating system.
....
<!-- more-->

## What is happening...

Today I start my linux , it prompt
```
    grub rescue>
```
Then I don't know what to do, then google it, then do as the following:
    
```
    grub rescue> ls
    grub rescue> ls (hd0,3)/boot
```
Then I know where my vmlinuz and initrd file locate.

Then do the following:
```
    grub rescue> set prefix=(hd0,2)/boot/grub
    grub rescue> insmod(hd0,2)/boot/grub/linux.mod
    grub rescue> insmod part_msdos (maybe not need)
    grub rescue> insmod ext2
    grub rescue> insmod gzip
    grub rescue> set root=(hd0,2)
    grub rescue> linux /boot/vmlinuz-3.0.0-*** root=/dev/sda3 ro
    grub rescue> initrd /boot/initrd.img-3.0.0-***
```

Then boot your system again:
```
    grub rescue> boot
```

OK, that's all, may be you can start your linux system, into the system, you can fix your grub.
........
