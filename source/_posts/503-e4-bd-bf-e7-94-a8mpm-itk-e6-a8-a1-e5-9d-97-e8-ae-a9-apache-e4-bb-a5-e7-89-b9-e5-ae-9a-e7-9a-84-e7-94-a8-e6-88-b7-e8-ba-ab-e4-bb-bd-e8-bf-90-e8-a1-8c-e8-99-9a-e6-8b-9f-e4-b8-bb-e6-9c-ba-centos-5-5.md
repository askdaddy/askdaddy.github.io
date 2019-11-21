---
title: 使用mpm-itk让 apache 以特定的用户身份运行虚拟主机
tags:
  - httpd
url: 503.html
id: 503
categories:
  - linux server
date: 2012-12-12 13:39:34
---

[使用mpm-itk模块让 apache 以特定的用户身份运行虚拟主机 ](http://blog.csdn.net/sondx/article/details/7576134) 1.安装 \[bash\] rpm -Uvh http://repo.webtatic.com/yum/centos/5/latest.rpm yum install--enablerepo=webtatic httpd httpd-itk \[/bash\] 2.配置 \[bash\] vi /etc/sysconfig/httpd \[/bash\] \[text\] HTTPD=/usr/sbin/httpd.itk \[/text\] \[bash\] vi /etc/httpd/conf.d/php.conf \[/bash\] \[text\] <IfModule itk.c> LoadModule php5_module modules/libphp5.so </IfModule> \[/text\] 在 <VirtualHost>标签里加上 \[text\] AssignUserId goup users \[/text\] 3.重启httpd