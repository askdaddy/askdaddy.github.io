---
title: 修改mysql root密码
url: 83.html
id: 83
categories:
  - 'NULL'
date: 2008-04-01 02:16:00
tags:
---

mysql密码丢失后，在mysql命令行下执行如下命令，即可将root用户密码清空：  
  
　　mysqld_safe --skip-grant-tables&  
  
mysql修改密码  
  
　　mysql修改，可在mysql命令行执行如下：  
  
　　mysql -u root mysql  
　　mysql> UPDATE user SET password=PASSWORD("new password") WHERE user='root';  
　　mysql> FLUSH PRIVILEGES;  
　　mysql> QUIT  

humen1 Tech