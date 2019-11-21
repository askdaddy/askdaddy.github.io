---
title: ubuntu 中把ppk转换成 openssh key
tags:
  - ssh
url: 683.html
id: 683
categories:
  - linux桌面
date: 2013-12-17 10:22:53
---

先装putty tool \[sh\] sudo apt-get install putty-tools \[/sh\] 然后转换 \[sh\] #private key puttygen /path/to/puttykey.ppk -O private-openssh -o id\_rsa #public key puttygen /path/to/puttykey.ppk -O public-openssh -o id\_rsa.pub \[/sh\]