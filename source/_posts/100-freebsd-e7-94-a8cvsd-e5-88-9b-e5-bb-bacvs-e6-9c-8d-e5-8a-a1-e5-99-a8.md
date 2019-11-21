---
title: FreeBSD 用cvsd创建cvs服务器
tags:
  - unix
url: 100.html
id: 100
categories:
  - 'NULL'
date: 2008-02-19 20:59:00
---

1\. 下载及安装

用ports 安装cvsd,位于 /usr/ports/devel/cvsd  
用ports 安装cvs,位于 /usr/ports/devel/cvs ipv6

创建 cvsd 用户(#useradd)。  

2\. 修改配置

指定虚拟根目录的实际路径，在RootJail命令后设置  
/usr/local/etc/cvsd/cvsd.conf

\# RootJail  
\# This is the location of the chroot jail  
\# cvs should be run in.  
\# Specify @#none@# (without quotes) to not use  
\# a chroot jail.  
\# This directory should be initialized with  
\# the cvsd-buildroot script.  
RootJail /home/soft/cvsd

创建 /home/soft/cvsd,  
使用命令行 /usr/local/sbin/cvsd-buildroot /home/soft/cvsd/ 初始化虚根目录

创建cvsroot 目录 : mkdir /home/soft/cvsd/cvsroot

用命令 cvs -d /home/soft/cvsd/cvsroot init 初始化cvs目录

用命令建立cvs用户:  
cvsd-passwd /home/soft/cvsd/cvsroot/ cvsuser:cvsd  
上面的命令建立cvsuer 这个帐号，它和系统的 cvsd用户挂接。注意，cvsd是操作系统的用户名,是第一步操作中建立的。  
你还可以使用该命令建立其它帐号.

将cvsroot 加入/usr/local/etc/cvsd/cvsd.conf的最后一行,如下面  
Repos /cvsroot

此句指明要使用虚拟根下的 "cvsroot" 这个仓库。  

3 设置启动脚本  
#echo cvsd_enable="YES" >> /etc/rc.conf

#reboot

4.注意事项

cvsd只是cvs的一个外壳程序，将cvs运行在虚拟根环境下，提高系统的安全性。你在安装cvsd后还必须安装cvs程序。  

不要跨分区建立仓库，否则会提示找不到用户.  
我的/home 和/ 是两个不同的分区.我开始在home下创建仓库,在var下创建虚根目录,作了符号链接后不能读取文件.

声明:

转载此文请保留此声明信息。

驱动开发网 华语地区核心层开发专业网站 [http://www.driverdevelop.com](http://www.driverdevelop.com)

软件创造价值，驱动提供力量!

humen1 Tech