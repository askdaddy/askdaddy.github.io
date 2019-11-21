---
title: apache22 链接数设定
url: 55.html
id: 55
categories:
  - linux server
date: 2008-07-17 23:36:00
tags:
---

网上google了一下都是一篇老文说的是apache1.x和apache2.x的配置

从apache2.2开始，配置内容不仅仅存在于httpd.conf中了，httpd.conf中只存放了一些简单的支持和关联等配置。  
更多的设置放在了extra目录下的不同.conf文件中。

仅对最大连接数进行说明：  
MaxKeepAliveRequests语句被放置在了httpd-default.conf中  
MaxClients在httpd-mpm.conf中的三个模块beos,prefork,worker中分别进行设置  
我没有看到ServerLimit设置语句，于是在MaxClients之前手动加了进去。

apache2.2默认最大连接支持20000，如果要设置更大的连接，需要修改源代码并且重新进行编译。

humen1 Tech