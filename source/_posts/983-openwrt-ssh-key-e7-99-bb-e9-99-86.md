---
title: openwrt  ssh-key 登陆
url: 983.html
id: 983
categories:
  - 随笔
date: 2016-10-05 22:34:22
tags:
---

linux上公钥的位置在 ~/.ssh/authorized_keys 但是openwrt毕竟不是linux，auth keys 位置放在  /etc/dropbear 目录下 so， 执行以下命令即可

ln -s ~/.ssh/authorized\_keys /etc/dropbear/authorized\_keys
============================================================