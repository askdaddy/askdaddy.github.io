---
title: linux下直接用命令转换Unixtime
tags:
  - linux
url: 401.html
id: 401
categories:
  - linux桌面
date: 2011-05-03 14:06:36
---

一般我们都是用date这个命令来看时间和设置服务器时间，其实他还可以在各种时间格式间转换。 传统的从u转时间的命令是： #date -u --date="1970-01-01 1187769064 sec GMT" 还有中快捷方式 #date -d @1187769064