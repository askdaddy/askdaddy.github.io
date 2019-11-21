---
title: 'vsftpd出现 500 OOPS: cannot change directory 的解决办法'
tags:
  - vsftp
url: 792.html
id: 792
categories:
  - linux server
date: 2014-05-22 16:04:38
---

我是用了虚拟用户的方案，出现这个问题是因为SElinux 没有关闭。 关闭： \[bash\] $ setenforce 0 \[/bash\]