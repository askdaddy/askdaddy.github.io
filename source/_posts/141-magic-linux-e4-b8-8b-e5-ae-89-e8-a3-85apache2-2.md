---
title: magic linux下安装apache2.2
tags:
  - linux
url: 141.html
id: 141
categories:
  - 'NULL'
date: 2007-11-22 23:59:00
---

下载Apache服务器的最新稳定发布版本,官方下载地址是：http://httpd.apache.org/download.cgi。  
1、 下载源码文件httpd-2.2.6.tar.gz 到linux服务器的某个目录。  
2、 解压文件 # tar zxvf httpd-2.2.6.tar.gz .  
3、 配置 # ./configure –refix=/usr/local/apache22 //指定安装目录，以后要删除安装就只需删除这个目录。  
4、 编译和安装。 # make ; make install .  
5、 编写启动脚本，把它放到目录 /etc/rc.d/init.d/里，这里取名为httpd,其内容如下：  
#!/bin/bash  
#description:http server  
#chkconfig: 235 98 98  
case "$1" in  
start)  
echo "Starting Apache daemon..."  
/usr/local/apache2/bin/apachectl -k start  
;;  
  
stop)  
echo "Stopping Apache daemon..."  
/usr/local/apache2/bin/apachectl -k stop  
;;  
  
restart)  
echo "Restarting Apache daemon..."  
/usr/local/apache2/bin/apachectl -k restart  
;;  
  
status)  
statusproc /usr/local/apache2/bin/httpd  
;;  
  
*)  
echo "Usage: $0 {start|stop|restart|status}"  
exit 1  
;;  
Esac  
  
注意：#description:http server 这一行必须加上，否则在执行命令 # chkconfig –add httpd 时会出现“service apache does not support chkconfig”的错误报告。#chkconfig: 2345 98 98 表示在执行命令 # chkconfig –add httpd 时会在目录 /etc/rc2.d/ 、/etc/rc3.d/ /etc/rc5.d 分别生成文件 S98httpd和 K98httpd。这个数字可以是别的。  
  
6、 执行命令 # chkconfig --add httpd ，进入目录/etc/rc3.d/检查是否生成文件 S98httpd及K98httpd.  
7、 启动服务 # /usr/local/apache22/bin/httpd -k start

humen1 Tech