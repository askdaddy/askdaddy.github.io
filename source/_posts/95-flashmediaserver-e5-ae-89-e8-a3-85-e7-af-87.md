---
title: FlashMediaServer安装篇
tags:
  - linux
url: 95.html
id: 95
categories:
  - 'NULL'
date: 2008-01-16 11:37:00
---

FlashMediaServer安装篇  
1、下载fms2安装程序，点击下载  
[http://www.flashcom.com.cn/tools/FlashMediaServer2.tar.gz](http://www.flashcom.com.cn/tools/FlashMediaServer2.tar.gz)  
2、安装：

tar zxvf FlashMediaServer2.tar.gz

cd FMS\_2\_0\_1\_r27_linux

./installFMS -platformWarnOnly

说明：-platformWarnOnly，忽略安装平台，因为有些系统会安装不了，所以这个一定要加上。执行安装程序后会有些类似于同意条款之类的东西，直接ctrl+c就得，然后需要填写一些配置，一般默认就可以，我填的是这样的：

Installation directory         = /opt/macromedia/fms //安装目录

FMS Server Port                = 1935  //服务端口  
FMS Admin Server Port          = 1111 //管理端口

Administrative username        = yingzi //管理员

Administrative password        = (suppressed) //管理员密码

FMS owner                      = root

FMS service user               = root

FMS service user group         = root

FMS run as daemon              = Yes  
Start FMS                      = Yes

3、启动和停止

启动：

./fmsmgr server fms start

./fmsmgr adminserver start

  
停止：

./fmsmgr server fms stop

./fmsmgr adminserver stop

humen1 Tech