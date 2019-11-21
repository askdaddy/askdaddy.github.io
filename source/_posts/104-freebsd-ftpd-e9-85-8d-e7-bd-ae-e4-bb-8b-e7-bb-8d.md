---
title: freeBSD ftpd配置介绍
tags:
  - unix
url: 104.html
id: 104
categories:
  - 'NULL'
date: 2008-01-29 11:55:00
---

像自带sendmail一样，freeBSD在系统安装时自带了ftp，这就是freeBSD的ftpd进程，默认以inetd方式运行，你只要在/etc/inetd.conf里如下设置：  
ftp stream tcp nowait root /usr/libexec/ftpd ftpd -l  
ftp stream tcp6 nowait root /usr/libexec/ftpd ftpd -l  
并在/etc/rc.conf里设置：  
inetd_enable="YES"  
这样ftpd就能顺畅运行。  
但是如果你的ftp运行很繁忙，用inetd方式运行ftp势必影响效率和性能，此时建议你以独立方式运行freeBSD的ftpd，方法很简单，如下：  
在/etc/inetd.conf里注释掉以上两句，用如下方式启动：  
#/usr/libexec/ftpd -D  
ftpd的参数比较多常用的如下：  
-A: 只允许匿名登录；  
-M: 不允许匿名创建目录；  
-m: 赋予匿名修改，覆盖等权限；  
更多参数请man ftpd.  
ftpd的相关设置文件：  
/etc/ftpusers List of unwelcome/restricted users.  
/etc/ftpchroot List of normal users who should be chroot'd.  
/etc/ftphosts Virtual hosting configuration file.  
/etc/ftpwelcome Welcome notice.  
/etc/ftpmotd Welcome notice after login.  
/var/run/nologin Displayed and access refused.  
/var/log/ftpd Log file for anonymous transfers.  
/var/log/xferlog Default place for session logs.

humen1 Tech