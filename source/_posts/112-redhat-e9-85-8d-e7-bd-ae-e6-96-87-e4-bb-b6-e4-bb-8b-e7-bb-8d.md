---
title: Redhat配置文件介绍
tags:
  - linux
url: 112.html
id: 112
categories:
  - 'NULL'
date: 2008-01-25 11:01:00
---

1./etc/sysconfig/mouse  
　　MOUSETYPE="ps/2"  
　　XMOUSETYPE="PS/2"  
　　FULLNAME="Generic 3 Button Mouse (PS/2)"  
　　XEMU3=no  
　　  
　　2\. /etc/sysconfig/network 网络配置文件  
　　NETWORKING=yes #肯定是YES，不用网络有必要使用LINUX吗？  
　　FORWARD_IPV4=no #IPV4转发，当你的机器作路由器时将此项设为yes  
　　HOSTNAME=[helius.dlut.edu.cn](http://helius.dlut.edu.cn)  
　　#主机名  
　　GATEWAY=[202.118.66.1](http://202.118.66.1)  
　　#默认网关（路由器）  
　　GATEWAYDEV=eth0 #与默认网关在同一物理网上的网卡逻辑设备名  
　　#对于大多数用户应该是eth0,除非你的机器作路由或有两块以上网卡  
　　  
　　3./etc/sysconfig/soundcard  
　　# THIS FILE IS WRITTEN BY SNDCONFIG  
　　# PLEASE USE SNDCONFIG TO MODIFY  
　　# TO CHANGE THIS FILE!  
　　# There should be no spaces at the start of a line  
　　# or around the '=' sign  
　　CARDTYPE=SB32  
　　  
　　4\. /etc/sysconfig/sendmail  
　　sendmail启动参数，具体参数请参考系统启动文件、sendmail文档及FAQ，示例文件内容如下：  
　　  
　　DAEMON=yes  
　　QUEUE=1h  
　　  
　　5\. /etc/sysconfig/static-routes  
　　静态路由表配置文件，可使用linuxconf或control-pannel配置并生成此文件，格式如下：  
　　  
　　网卡逻辑设备名 传送给route命令的参数(不带add)  
　　  
　　示例文件格式如下：  
　　  
　　eth0 net [202.118.68.0](http://202.118.68.0) netmask [255.255.252.0](http://255.255.252.0) gw [202.118.66.16](http://202.118.66.16)  
　　eth0 net [202.118.65.0](http://202.118.65.0) netmask [255.255.255.0](http://255.255.255.0) gw [202.118.66.13](http://202.118.66.13)  
　　eth0 net [202.199.128.0](http://202.199.128.0) netmask [255.255.240.0](http://255.255.240.0) gw [202.118.66.253](http://202.118.66.253)  
　　  
　　6\. /etc/sysconfig/pcmcia  
　　PCMCIA卡配置文件，台式机上不用配置此文件，示例文件内容如下：  
　　  
　　PCMCIA=no  
　　PCIC=  
　　PCIC_OPTS=  
　　CORE_OPTS=  
　　  
　　  
　　6\. /etc/sysconfig/network-scripts/* 网络配置启动文件及参数配置  
　　  
　　ifcfg-* 相应网络接口网络配置，如eth0对应文件ifcfg-eth0,内容如下：  
　　#以后为注释，配置文件中不用加  
　　  
　　文件ifcfg-eth0  
　　  
　　DEVICE=eth0 #此设备名一定要和文件名中的设备名对应，如ifcfg-eth1文件中此  
　　#设备名为eth1  
　　IPADDR=[202.118.66.81](http://202.118.66.81) #IP地址  
　　NETMASK= [255.255.255.0](http://255.255.255.0) #网络屏蔽位，通常为255.255.255.0  
　　NETWORK=[202.118.66.0](http://202.118.66.0) #网络地址，在网络屏蔽位是255.255.255.0时将IP地址最后  
　　#一位设为0即可  
　　BROADCAST=202.118.66.255#广播地址，在网络屏蔽位是255.255.255.0时将IP地址最后  
　　#一位设为255即可  
　　ONBOOT=yes  
　　BOOTPROTO=none  
　　  
　　此目录下除ifcfg-*之外，还有ifup-*，ifdown-*等文件，对于大多数用户而言，这  
　　些文件不用修改。  
　　  
　　  
　　7\. /etc/conf.modules  
　　此文件为内核模块配置文件，系统在启动时从此文件中读取网卡、声卡等设备的配置，  
　　具体说明请参考/usr/doc/HOWTO/下相应的说明文档。  
　　  
　　示例文件内容如下：  
　　  
　　alias eth0 tulip  
　　alias sound sb  
　　options opl3 io=0x388  
　　alias midi awe_wave  
　　post-install awe_wave /usr/bin/sfxload /etc/midi/GU11-ROM.SF2  
　　options sb io=0x220 irq=5 dma=1 dma16=5 mpu_io=0x330  

humen1 Tech