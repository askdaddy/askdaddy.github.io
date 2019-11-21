---
title: redhat下修改主机名
tags:
  - linux
url: 90.html
id: 90
categories:
  - 'NULL'
date: 2007-12-26 14:17:00
---

#vi /etc/hosts 修改主机名  
#vi /etc/sysconfig/network，修改HOSTNAME一行为"HOSTNAME=主机名"(没有这行？那就添加这一行吧)，然后运行命令" hostname 主机名"。  
reboot 

humen1 Tech