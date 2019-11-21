---
title: mysql5 修改默认最大连接数
url: 48.html
id: 48
categories:
  - 'NULL'
date: 2008-10-07 15:41:00
tags:
---

  
在/etc下的 my.cnf文件中

\[mysqld\]区块中新增一句

max_connections = 768

  

  

然后重启数据库

  

#mysql -u user -p  
后

mysql>show variables;  
会看到max_connections 的值  

humen1 Tech