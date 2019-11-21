---
title: samba 配置
tags:
  - linux
url: 126.html
id: 126
categories:
  - 'NULL'
date: 2007-11-20 10:50:00
---

前言

SAMBA是一种能把 FreeBSD 的目录开放给Microsoft Windows 95/98/NT

利用网路芳邻方式存取的软体集。其实并不只针对 FreeBSD，

其它UN*X 也都可以使用，这对工作平台大部分时间是Microsoft family的人

在存取档案上，会是个比较方便的选择。

安装SAMBA 2.0.6

1.先以 root 身份 login，切换至/usr/ports/net/samba 准备安装SAMBA。

安装时只要在 SAMBA 的目录下执行 make install 即可

\# [root@ohaha](mailto:root@ohaha)\[~\] cd /usr/ports/net/samba/

\# [root@ohaha\[/usr/ports/net/samba](mailto:root@ohaha[/usr/ports/net/samba)\] make install

若无出现错误讯息则是安装完成，你可顺手将安装过程中解开的source清掉。

\# [root@ohaha\[/usr/ports/net/samba](mailto:root@ohaha[/usr/ports/net/samba)\] make clean

设定 SAMBA (smb.conf)

在安装完 SAMBA 後，它会放一份设定档例在/usr/local/etc 下，

先将例一份来修改成我们要的设定。

\# [root@ohaha](mailto:root@ohaha)\[~\] cd /usr/local/etc/

\# [root@ohaha\[/usr/local/etc](mailto:root@ohaha[/usr/local/etc)\] cp smb.conf.default smb.conf

sam.conf.default是设定 SAMBA 的例档，真正读取的预设是 smb.conf，

为了保留原始的例档以供日後参考用，所以我们用 cp 的方式出设定档，

大致浏览过 smb.conf 後发现，它主要分成三大设定区，\[globe\]、\[homes\]、

\[printers\]，我没有印表机，所以没机会试\[printers\]相关部分。

我开 SAMBA 的目地是为了方便存取管理 ftp 并使用该台 FreeBSD 上

的硬碟空间，所以等会设定档的最终目地便是开出一个分享目录 ftp，

无须密码，但只允许我的工作机器去存取它。

在 smb.conf 中，所有的＃和；都是解。＃後接的是说明，

；後接的是指令，预设不打开该项设定，若想让它生效把分号拿掉即可。

以下只引出我有动过的地方，没提出的就是保留预设值。

#======================= Global Settings =====================================

\[global\]

\# workgroup = NT-Domain-Name or Workgroup-Name, eg: REDHAT4

\# 设定所在工作群组

workgroup = center

\# server string is the equivalent of the NT Description field

\# 该主机的解

server string = blah~

\# This option is important for security. It allows you to restrict

\# connections to machines which are on your local network. The

\# following example restricts access to two C class networks and

\# the "loopback" interface. For more examples of the syntax see

\# the smb.conf man page

\# 允许连线的主机，允许 [163.16.1.99](http://163.16.1.99) 和 127.*.*.* 连线

hosts allow = [163.16.1.99](http://163.16.1.99) 127.

\# If you want to automatically load your printer list rather

\# than setting them up individually then you'll need this

\# 我没有 printer ，所以有关 printer 的都会关掉

; load printers = yes

\# Uncomment this if you want a guest account, you must add this to /etc/passwd

\# otherwise the user "nobody" is used

\# 这里设定免密码的帐号，你设什麽帐号，连进来的 client就是那个身份，了吗？

\# 所以我把这儿改成 ftp 这个帐号，因为我 share 出来的目录 owner 是 ftp

\# 这样我才能以免密码又是 ftp 的身份对目录有完整的存取权。

\# 不过记得，这儿填的帐号必须存在 /etc/passwd 中，否则会以 nobody 的身份签入。

guest account = ftp

\# this tells Samba to use a separate log file for each machine

\# that connects

\# 把 log 建个目录来放比较整齐，记得去 mkdir /var/log/samba 这个目录。

log file = /var/log/samba/log.%m

\# Security mode. Most people will want user level security. See

\# security_level.txt for details.

\# 设定安全层级，若要不用密码分享的话就要设成 share ，若设 user 的话会要求密码。

\# 详情请见 docs/security_level.txt

security = share

\# You may wish to use password encryption. Please read

\# ENCRYPTION.txt, Win95.txt and WinNT.txt in the Samba documentation.

\# Do not enable this option unless you have read those documents

\# 我的目的是不用密码存取，所以这项开不开都没影响，但若你想用密码来控制存取权限时，

\# 请记得将此项打开，因为...详见 docs/ENCRYPTION.txt, Win95.txt 和 WinNT.txt。

; encrypt passwords = yes

\# for Traditional Chinese Users

\# 若你想看到中文目录、档名的话，把 client code page=950 前的分号拿掉，

\# 注意，coding system 那项留着别打开它，两个都打开的话反而会看不到中文

client code page=950

; coding system=cap

#============================ Share Definitions ==============================

\# 接下来这一段就是 \[homes\] 和 \[printers\] 以及其它任何你想 share 出来的目录设定

\# 区，我把 \[homes\] 也 mark 起来了，因为我不想 share 任何 home 出来。

;\[homes-%U\]

; comment = Home Directories

; path = /home/%U

; user = %U

; browseable = no

; writeable = yes

\# ftp

\# 我加了这段，将 ftp 的目录开分享。一开始我们看到的 \[ftp\] 就是你分享出来的目录

\# 在 95/98/NT 中会看到的资料夹名称，path 指向欲 share 目录的绝对路径，

\# public = yes 是指定这个分享不须密码，writeable = yes 是指可对该分享做写入动作

\# 注意一点，当有 public = yes 这行时，对该分享存取的身份就是之前在 \[globe\] 区，

\# 我们所设定 guest account 的身份，若刚刚 guest account 没改成 ftp，那麽现在

\# 即使有设 writeable = yes 也会因为 owner 不对而无 法写入。

\[ftp\]

path = /home/ftp

public = yes

writeable = yes

启动 SAMBA

在安装完 SAMBA 後，它丢了个启动的 script 在 /usr/local/etc/rc.d/，

档名是 samba.sh.sample，将之更名并 chmod 成可执行。

\# [root@ohaha\[/usr/local/etc/rc.d](mailto:root@ohaha[/usr/local/etc/rc.d)\] mv samba.sh.sample samba.sh

\# [root@ohaha\[/usr/local/etc/rc.d](mailto:root@ohaha[/usr/local/etc/rc.d)\] chmod 750 samba.sh

你现在可以重新开机或者手动执行 samba.sh 来启动 SAMBA。

\# [root@ohaha](mailto:root@ohaha)\[~\] /usr/local/etc/rc.d/samba.sh  
 

humen1 Tech