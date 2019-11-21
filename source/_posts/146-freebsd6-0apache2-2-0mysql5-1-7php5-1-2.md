---
title: freebsd6.0+apache2.2.0+mysql5.1.7+php5.1.2
tags:
  - unix
url: 146.html
id: 146
categories:
  - 'NULL'
date: 2007-11-20 00:34:00
---

操作系统以及版本：freebsd6.0+apache2.2.0+mysql5.1.7+php5.1.2  
  
一、安装mysql51  
  
先添加mysql组和mysql用户  
  
QUOTE:pw addgroup mysqlpw adduser mysql开始安装  
  
QUOTE:cd /usr/ports/databases/mysql51-server/ make install clean # n长的编译过程 rehash cp /usr/local/share/mysql/my- large.cnf /etc/my.cnf #服务器内存1G，但是与apache在一起/usr/local/share/mysql下面有5个my-xxxx.cnf文件my-small.cnf 最小配置安装，内存<=64M，数据数量最少my-large.cnf 内存=512Mmy-medium.cnf 32M<内存<64M，或者内存有128M，但是数据库与web服务器公用内存 my-huge.cnf 1G<内存<2G，服务器主要运行mysqlmy-innodb-heavy-4G.cnf 最大配置安装，内存至少4G  
  
QUOTE:mysql\_install\_db -u mysql ; mysqld_safe -u mysql & #建立数据库目录二、安装apache22+php5  
  
QUOTE: cd /usr/ports/www/apache22/ make install clean cd ../mod_php5 make install clean 配置/usr/local/etc/apache/httpd.conf：加入  
  
QUOTE:AddType application/x-httpd-php .php AddType application/x-httpd-php-source .phps #可不加 *注意：第二行主要为查看php代码用，加上的话web目录下的所有扩展名为.phps的文件在被浏览器访问时都显示其源代码，我安装的时候就加了，但少了.phps的s，之后郁闷了半天  
  
QUOTE:DocumentRoot "/usr/local/www/apache22/data" 这两个是你的主页目录，可以根据自己需要跟改，要一致。  
  
QUOTE: Options Indexes FollowSymLinks去掉Indexes可以限制浏览你的主页目录  
  
QUOTE:rehash apachectl start echo "" \> /usr/loacl/www/data/info.php 可能你的apache启动的时候和我一样会报这样的错误：  
  
QUOTE:\[Wed Apr 12 21:48:09 2006\] \[warn\] (2)No such file or directory: Failed to enable the 'httpready' Accept Filter我在google上找到了解决办法，执行如下操作：  
  
QUOTE:kldload accf_http  
  
grep accf /boot/defaults/loader.confaccf\_data\_load="NO" # Wait for data accept filteraccf\_http\_load="NO" # Wait for full HTTP request accept filter #将这个"NO"改成"YES" 但是为什么这样做还不知道，而且这个accf是做什么用的也不知道，还请大侠们来解释一下。  
  
访问http://服务器的IP/info.php，如果有php的说明文件说明基本的php+apache2已经工作正常！  
  
php5扩展功能安装  
  
QUOTE:cd /usr/port/lang/php5-extensions/ make install clean #如果第一次安装会出现提示框，否则先make conf设置 选择需要的模块，当然也可以选择必须的，日后再添加。  
  
apachectl restart 如果http://服务器ip/info.php有改动，恭喜你！安装成功！！  
  
后续工作：  
  
QUOTE:echo ' mysql\_enable = "YES" ' >> /etc/rc.conf echo ' apache22\_enable="YES" ' >> /etc/rc.conf 以便开机后自动启动mysql apache

humen1 Tech