---
title: '更改ssh端口[Freebsd]'
tags:
  - unix
url: 134.html
id: 134
categories:
  - 'NULL'
date: 2007-12-17 14:14:00
---

配置文件位置

/etc/ssh/sshd_config

在配置文件中搜索 Port

修改为

Port 2222

*2222为我要修改的当前端口，确保没有被使用。ssh原来的默认端口是22  
  
 

humen1 Tech