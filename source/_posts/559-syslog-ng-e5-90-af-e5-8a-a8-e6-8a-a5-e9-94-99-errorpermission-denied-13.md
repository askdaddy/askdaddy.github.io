---
title: 'syslog-ng 启动报错 [ error=''Permission denied (13)'' ]'
url: 559.html
id: 559
categories:
  - linux server
date: 2013-04-01 14:15:41
tags:
---

配置了远程记录日志，重启后报错，配置没有问题，所以不贴了，报错内容如下： \[bash\] 启动 syslog-ng：Error binding socket; addr='AF\_INET(0.0.0.0:6000)', error='Permission denied (13)' Error initializing source driver; source='s\_test2\_network', id='s\_test2_network#0' Error initializing message pipeline; \[失败\] \[/bash\] 问题出在 SELinux上，关掉就OK 特此记录。