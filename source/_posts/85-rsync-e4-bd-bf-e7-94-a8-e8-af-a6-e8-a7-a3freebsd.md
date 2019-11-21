---
title: 'RSYNC使用详解[freebsd]'
url: 85.html
id: 85
categories:
  - 'NULL'
date: 2008-03-31 17:46:00
tags:
---

RSYNC使用详解  
目的是同步两台主机上的文件  
主机A ：[192.168.1.200](http://192.168.1.200)  
主机B：[192.168.1.201](http://192.168.1.201)  
环境还是freebsd 6.2  
  
1.先安装rsync 我用ports装（两台都装）  
  
\# cd /usr/ports/net/rsync  
\# make install clean  
  
2.配置服务端192.168.1.200  
\# vi /usr/local/etc/rsyncd.conf  
  
\[data_www\]              ///模块名称---也就一个需要同步或备份的目录  
   path = /data/www  //要同步的目录  
   comment = home cad folder //描述  
   ignore errors  
   read only = yes  
   list = no  
   auth users = backup             ////登录用户名  
   secrets file = /usr/local/etc/rsyncd.pass  ////密码存放文件  
  
  
  
/************************************/  
/usr/local/etc/rsyncd.pass  
密码格式如下  
   用户名：密码 （有个冒号哟）  
我是这样设定的  
backup:123456  
  
!!!!!!!!出于安全目的，文件的属性必需是只有属主可读(不能错)!!!!!!!!!!!!!!!!!    
  
 chmod 600 /usr/local/etc/rsyncd.pass  
  
3.启动服务  
\# rsync --daemon  
开机启动这样配置  
  
配置文件 /etc/rc.conf  
  
加入rsyncd_enable="YES"  
  
  
4.配置客户端192.168.1.201  
要避免在同步时交互输入密码，我们先把密码放在一个文件里  
我用了和服务端一样的文件名和路径/usr/local/etc/rsyncd.pass  
但是内容不同，在服务端格式是 用户名:密码。在客户端我们就只要密码就好  
于是写入    
123456  
  
#chmod 600 /usr/local/etc/rsyncd.pass  
  
我们再写个shell脚本用来快速执行  
  
#vi /etc/sh/rsync_data.sh  
写入以下内容  
  
/usr/local/bin/rsync -vzrtopg --progress  --delete --password-file=/usr/local/etc/rsyncd.pass /data/www/ backup@192.168.1.200::data_www  
  
ok现在来同步  
  
\# /etc/sh/rsync_data.sh  
这样主机B 的/data/www目录的内容就会同步到主机A了。  
  

humen1 Tech