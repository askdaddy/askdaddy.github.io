---
title: 'Mysql 主从镜像机制[freebsd]'
tags:
  - unix
url: 136.html
id: 136
categories:
  - 'NULL'
date: 2007-12-18 16:55:00
---

测试用例

主机和从机配置完全一样。环境vm5.5.3 Freebsd6.2 Mysql-5.1.4

master : [192.168.1.71](http://192.168.1.71)  
slave  : [192.168.1.72](http://192.168.1.72)

mysql是ports默认设置安装的  
数据文件在/var/db/mysql/下

1.主机配置  
#mysql -u root -p  
#Enter password:

mysql>GRANT FILE,SELECT,REPLICATION SLAVE ON *.* TO [seven@192.168.1.72](mailto:seven@192.168.1.72) IDENTIFIED BY 'seven';  
mysql> flush tables with read lock;  
mysql> show master status;  
+------------------+----------+--------------+------------------+  
| File             | Position | Binlog\_Do\_DB | Binlog\_Ignore\_DB |  
+------------------+----------+--------------+------------------+  
| mysql-bin.000035 |      106 |              |                  |  
+------------------+----------+--------------+------------------+  
1 row in set (0.01 sec)  
记下file & position

mysql>exit  
#/usr/local/etc/rc.d/mysql_server stop

#ee /etc/my.cnf

\[mysqld\]下  
server-id=1  
log-bin=mysql-bin #log文件名

2.从机配置

#ee /etc/my.cnf  
\[mysqld\]下  
server-id=2

重启mysql  
#mysql -u root -p  
#Enter password:

mysql>CHANGE MASTER TO  
    ->     MASTER_HOST='[192.168.1.71](http://192.168.1.71)',           \-\- 主服务器名或IP地址  
    ->     MASTER_USER='seven',               
    ->     MASTER_PASSWORD='seven',  
    ->     MASTER\_LOG\_FILE='mysql-bin.000035',    -- 日志名  
    ->     MASTER\_LOG\_POS=106;                    -- 显示偏移量       
mysql>START SLAVE;                                -- 启动从服务器线程

  
-----重启2台服务器-----

******测试*****  
在主服务器（1.71）数据库上做如下操作:  
mysql> show processlist\\G  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* 1\. row ***************************  
     Id: 1  
   User: root  
   Host: localhost  
     db: NULL  
Command: Query  
   Time: 0  
  State: NULL  
   Info: show processlist  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* 2\. row ***************************  
     Id: 2  
   User: seven  
   Host: [192.168.1.72:56493](http://192.168.1.72:56493)  
     db: NULL  
Command: Binlog Dump  
   Time: 510  
  State: Has sent all binlog to slave; waiting for binlog to be updated  
   Info: NULL  
2 rows in set (0.01 sec)

  
在从服务器（1.72）数据库上做如下操作:

mysql> show processlist\\G  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* 1\. row ***************************  
     Id: 1  
   User: system user  
   Host:  
     db: NULL  
Command: Connect  
   Time: 577  
  State: Waiting for master to send event  
   Info: NULL  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* 2\. row ***************************  
     Id: 2  
   User: system user  
   Host:  
     db: NULL  
Command: Connect  
   Time: 451  
  State: Has read all relay log; waiting for the slave I/O thread to update it  
   Info: NULL  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* 3\. row ***************************  
     Id: 3  
   User: root  
   Host: localhost  
     db: NULL  
Command: Query  
   Time: 0  
  State: NULL  
   Info: show processlist  
3 rows in set (0.01 sec)

  
还可以使用。。。。

查看主机状态  
mysql> show master status\\G  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* 1\. row ***************************  
            File: mysql-bin.000022  
        Position: 453  
    Binlog\_Do\_DB:  
Binlog\_Ignore\_DB:  
1 row in set (0.00 sec)

查看从服务器状态  
mysql> show slave status\\G  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* 1\. row ***************************  
               Slave\_IO\_State: Waiting for master to send event  
                  Master_Host: [192.168.1.71](http://192.168.1.71)  
                  Master_User: seven  
                  Master_Port: 3306  
                Connect_Retry: 60  
              Master\_Log\_File: mysql-bin.000022  
          Read\_Master\_Log_Pos: 453  
               Relay\_Log\_File: bsd_s-relay-bin.000009  
                Relay\_Log\_Pos: 598  
        Relay\_Master\_Log_File: mysql-bin.000022  
             Slave\_IO\_Running: Yes  
            Slave\_SQL\_Running: Yes  
              Replicate\_Do\_DB:  
          Replicate\_Ignore\_DB:  
           Replicate\_Do\_Table:  
       Replicate\_Ignore\_Table:  
      Replicate\_Wild\_Do_Table:  
  Replicate\_Wild\_Ignore_Table:  
                   Last_Errno: 0  
                   Last_Error:  
                 Skip_Counter: 0  
          Exec\_Master\_Log_Pos: 453  
              Relay\_Log\_Space: 898  
         &nbs p;    Until_Condition: None  
               Until\_Log\_File:  
                Until\_Log\_Pos: 0  
           Master\_SSL\_Allowed: No  
           Master\_SSL\_CA_File:  
           Master\_SSL\_CA_Path:  
              Master\_SSL\_Cert:  
            Master\_SSL\_Cipher:  
               Master\_SSL\_Key:  
        Seconds\_Behind\_Master: 0  
Master\_SSL\_Verify\_Server\_Cert: No  
                Last\_IO\_Errno: 2013  
                Last\_IO\_Error: error connecting to master ['seven@192.168.1.71:3306'](mailto:'seven@192.168.1.71:3306') \- retry-time: 60  retries: 86400  
               Last\_SQL\_Errno: 0  
               Last\_SQL\_Error:  
1 row in set (0.00 sec)  
 

humen1 Tech