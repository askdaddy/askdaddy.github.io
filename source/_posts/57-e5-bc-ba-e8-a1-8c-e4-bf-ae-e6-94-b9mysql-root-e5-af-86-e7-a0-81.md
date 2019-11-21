---
title: 强行修改mysql root 密码
url: 57.html
id: 57
categories:
  - 'NULL'
date: 2008-07-09 11:16:00
tags:
---

如果mysql正在运行  
首先杀之： killall -TERM mysqld  
以安全模式启动mysql  
#/usr/local/bin/mysqld_safe --skip-grant-tables &  
进入控制台  
#mysql  
>use mysql  
>update user set password=password("new_pass") where user="root";  
>flush privileges;  
重新杀 MySQL进程 ，用正常方法启动 MySQL

humen1 Tech