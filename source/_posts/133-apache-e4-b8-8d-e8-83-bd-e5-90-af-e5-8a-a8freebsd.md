---
title: 'apache 不能启动[Freebsd]'
tags:
  - unix
url: 133.html
id: 133
categories:
  - 'NULL'
date: 2007-12-17 14:56:00
---

  

启动 httpd 时出现  
Starting httpd: httpd: apr\_sockaddr\_info_get() failed for MYHOST  
httpd: Could not reliably determine the server's fully qualified domain name, using [127.0.0.1](http://127.0.0.1/) for ServerName.

这个问题是没有在 /etc/httpd/conf/httpd.conf 中设定 ServerName ，  
所以它会用主机上的名称来取代，首先会去找/etc/hosts中有没有主机的定义  
解决方式：  
1.设定 ServerName  
2.在 /etc/hosts 中填入主机名MYHOST：

>ee /etc/hosts

[127.0.0.1](http://127.0.0.1/) localhost.localdomain localhost MYHOST

  
 

humen1 Tech