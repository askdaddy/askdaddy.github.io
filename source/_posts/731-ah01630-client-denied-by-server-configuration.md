---
title: 'AH01630: client denied by server configuration'
tags:
  - apache
  - http
  - linux
  - web
url: 731.html
id: 731
categories:
  - linux server
date: 2014-01-26 11:02:22
---

升级到apache2.4 配置语法也变了 Order Allow, Deny Allow from all 需要改为： Require all granted 这样问题就解决了