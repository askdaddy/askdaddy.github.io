---
title: 关于 Redhat9 的网络配置文件
tags:
  - linux
url: 114.html
id: 114
categories:
  - 'NULL'
date: 2008-01-25 14:37:00
---

完整搜索顺序是：（*为接口名）

  

/etc/sysconfig/networking/profiles/default/ifcfg-*  
/etc/sysconfig/networking/profiles/default/*  
/etc/sysconfig/networking/default/ifcfg-*  
/etc/sysconfig/networking/default/*  
/etc/sysconfig/network-scripts/ifcfg-*  
/etc/sysconfig/network-scripts/*

从上往下，找到任何一个就忽略其他。具体某人的机器这些配置放在哪里？是由你运行的网络接口配置程序决定的（linux有N多网络配置程序，像早些的netconf,netconfig,ifconfig,现在的X中gnome的配置程序，kde也有，redhat有个专用的redhat-config-network），程序作者想把它们放在哪里就是哪里，但一定是上面的范围。

humen1 Tech