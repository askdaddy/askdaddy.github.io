---
title: mysql 初始化@centos7
url: 935.html
id: 935
categories:
  - MySQL
date: 2016-01-14 23:36:04
tags:
---

mysql 初始化@centos7
=================

> rm -rf /var/lib/mysql mysqld –initialize-insecure –user=mysql systemctl start mysqld mysql -u root –skip-password