---
title: centos 网络配置
tags:
  - linux
url: 68.html
id: 68
categories:
  - 'NULL'
date: 2008-03-26 20:25:00
---

在centos系统的 /etc/sysconfig/network-script/ifcfg-eth0文件中存放着这台机子网卡IP地址配置的相关信息，它的具体格式为：  
\[root@localhost network-scripts\]# cat ifcfg-eth0  
DEVICE=eth0  
BOOTPROTO=none  
ONBOOT=yes  
TYPE=Ethernet  
NETMASK=[255.255.255.128](http://255.255.255.128)  
IPADDR=[11.19.13.16](http://11.19.13.16)  
USERCTL=no  
PEERDNS=yes  
GATEWAY=[61.49.23.129](http://61.49.23.129)  
只要我们按照上面的格式配置好文件的各个数据项，且用  
/etc/init.d/network reload 命令 或  
service network reload  
重新导入该文件，我们就可以将我们的网络启动起来。  
  

humen1 Tech