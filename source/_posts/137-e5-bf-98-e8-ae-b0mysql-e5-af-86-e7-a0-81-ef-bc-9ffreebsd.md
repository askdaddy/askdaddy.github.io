---
title: '忘记mysql密码？[freebsd]'
tags:
  - unix
url: 137.html
id: 137
categories:
  - 'NULL'
date: 2007-12-18 10:08:00
---

  
#killall mysqld  
#/usr/local/bin/mysqld_safe --skip-grant-tables &  
#mysql  
...  
mysql>use mysql  
mysql>update user set password=password("root") where user="root";  
mysql>flush privileges;  
mysql>exit

#killall mysqld

#/usr/local/etc/rc.d/mysql_server start

#mysql -u root -p  
#Enter password: root  
mysql>

humen1 Tech