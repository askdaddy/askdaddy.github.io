---
title: Disable IPv6 on ssh client
url: 1081.html
id: 1081
comments: false
categories:
  - 随笔
date: 2017-12-10 17:59:56
tags:
---

问题起于我要经ssh 连git.dn42.us, 比较特别的是我的机器（vps）上启用了IPv6

  

OpenSSH_7.2p2 Ubuntu-4ubuntu2.2, OpenSSL 1.0.2g  1 Mar 2016

debug1: Reading configuration data /home/seven/.ssh/config

debug1: /home/seven/.ssh/config line 1: Applying options for *

debug1: Reading configuration data /etc/ssh/ssh_config

debug1: /etc/ssh/ssh_config line 19: Applying options for *

debug1: Connecting to git.dn42.us \[2607:5300:60:3d95::1\] port 22.

  

以上是ssh的输出。 可以看到是通过IPv6连接的，死活不通。

于是禁用IPv6

  

# ~/.ssh/config

Host *

    AddressFamily inet

  

It works fine.