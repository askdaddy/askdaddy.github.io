---
title: Centos NFS
url: 11.html
id: 11
categories:
  - 技术杂文
date: 2009-03-24 10:12:00
tags:
---

centos nfs

<\-\- server:192.168.1.73 -->

\[root@localhost\]# cat /etc/sysconfig/network  
NETWORKING=yes  
HOSTNAME=localhost.localdomain

\[root@localhost\]#cat /etc/hosts  
127.0.0.1 localhost.localdomain localhost  
192.168.1.76 client.localdomain client

//开机启动nfs server  
\[root@localhost\]#chkconfig nfs on

//启动nfs  
\[root@localhost\]# mkdir /data/cache  
\[root@localhost\]# vi /etc/exports  
/data/cache/ 192.168.1.76(rw,no\_root\_squash,no\_all\_squash,sync)

<\-\- client:192.168.1.76 -->

bsd#mkdir /data/cache/  
bsd#mount 192.168.1.73:/data/cache /data/cache

  
//开机挂载  
bsd#vi /etc/fstab

//加入下行  
192.168.1.73:/data/cache /data/cache nfs rw 0 0

humen1 Tech![](https://blogger.googleusercontent.com/tracker/7269874978253342363-4145120966768541643?l=www.humen1.net)