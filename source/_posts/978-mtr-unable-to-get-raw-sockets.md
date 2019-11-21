---
title: 'mtr: unable to get raw sockets'
tags:
  - homebrew
  - mac
  - mtr
url: 978.html
id: 978
categories:
  - 随笔
date: 2016-06-21 13:34:40
---

mtr: unable to get raw sockets
==============================

`TECH``posts``Mac``homebrew``mtr` 用homebrew安装mtr 后有段提示：mtr requires root privileges so you will need to run `sudo mtr`. You should be certain that you trust any software you grant root privileges. 所以要吧mtr改成root属主并且激活suid位

    1.  $ sudo chown root:wheel /usr/local/Cellar/mtr/0.86/sbin/mtr2.  $ sudo chmod u+s /usr/local/Cellar/mtr/0.86/sbin/mtr