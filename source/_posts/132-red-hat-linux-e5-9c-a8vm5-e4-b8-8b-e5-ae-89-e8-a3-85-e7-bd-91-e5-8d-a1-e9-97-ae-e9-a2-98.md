---
title: red hat linux 在vm5下安装网卡问题
tags:
  - linux
url: 132.html
id: 132
categories:
  - 'NULL'
date: 2007-12-04 09:42:00
---

  
VMware以上和Redhat 9以上之间，网卡驱动有些不兼容：Redhat 9.0作Guest OS时，用"ifconfig eth0 up"是无法激活虚拟网卡的，总是提示诸如 "Determining IP information for eth0... failed; no link present. Check cable?"  
  
　　原因貌似是VMware提供的虚拟网卡驱动有一点点问题，解决办法在VMware的论坛里面提到过了：  
  
　　以root权限，编辑 /etc/sysconfig/network-scripts/ifcfg-ethx  
　　其中x是数字，比如eth0。在文件中添加：  
  
　　check\_link\_down () {  
　　 return 1;  
　　 }  
  
　　然后ifdown eht0 / ifup eth0 应该就可以了  
  

humen1 Tech