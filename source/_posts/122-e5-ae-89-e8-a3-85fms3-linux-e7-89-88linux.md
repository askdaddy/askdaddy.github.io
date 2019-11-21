---
title: '安装FMS3 Linux版[linux]'
tags:
  - linux
url: 122.html
id: 122
categories:
  - 'NULL'
date: 2008-03-14 23:42:00
---

之前在red hat linux 9上安装需要很多c的库依赖。看了adobe的官网fms3 适用于red hat 4 （也就是AS4版）但是不太想用redhat了，于是用了免费的CentOS  
对应的版本应该是centos4.2以上(AS4 update2)于是去下了个centOS4.6  
找了几处镜像以下链接是速度最快的（我用的是上海有线通）  
[http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin1of4.iso](http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin1of4.iso)  
[http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin2of4.iso](http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin2of4.iso)  
[http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin3of4.iso](http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin3of4.iso)  
[http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin3of4.iso](http://centos.candishosting.com.cn/4.6/isos/i386/CentOS-4.6-i386-bin3of4.iso)  
  
注意\* 第四张盘可以不用下，安装系统只要前三张盘  
  
  
centOS的安装我就不说了，我选择的是custom安装，牢记要选上开发工具选项，fms3的依赖包里有c++的列库依赖  
  
正式开始了  
  
  
先创建个用户和用户组给fms用  
  

\[root@seven ~\]# groupadd fms  
\[root@seven ~\]# useradd -g fms fms

  
将安装包放在随便哪个目录里解压（我放在 /share 里）  
  
\[root@seven ~\]# cd /share  
\[root@seven share\]# tar -xzf FlashMediaServer3.tar.gz  
  
...  
一阵解压后切到FMS3目录下  
  
\[root@seven share\]# cd /FMS\_3\_0\_0\_r1157  
\[root@seven FMS\_3\_0\_0\_r1157\]# ./installFMS -platformWarnOnly  
  
官方文档上写的只有 ./installFMS 这个行不通的装过2的人都知道  
  
安装过程和2差不多在 [2008 年 一月](http://www.humen1.net/2008_01_01_archive.html) 里有安装2的过程可以参考  
  
  
装好以后切到程序目录  
\[root@seven FMS\_3\_0\_0\_r1157\]# cd /opt/adobe/fms  
\[root@seven fms\] ./fmsmgr server fms start  
  
用top察看进程  
看到以下四个说明安装已成功了  

fmscore  
fmsedge  
fmsmaster  
fmsadmin

如果有什么问题比如跑不起服务试试看以下这些方法

1.有可能是其中一个依赖包没有

ldd fmsadmin  
linux-gate.so.1 => (0×00cea000)  
libpthread.so.0 => /lib/libpthread.so.0 (0×00721000)  
libasneu.so.1 => /usr/lib/libasneu.so.1 (0×00b68000)  
librt.so.1 => /lib/librt.so.1 (0×0074f000)  
libdl.so.2 => /lib/libdl.so.2 (0×0071b000)  
libstdc .so.6 => /usr/lib/libstdc .so.6 (0×04735000)  
libm.so.6 => /lib/libm.so.6 (0×006f2000)  
libgcc\_s.so.1 => /lib/libgcc\_s.so.1 (0×00dcb000)  
libc.so.6 => /lib/libc.so.6 (0×005b0000)  
/lib/ld-linux.so.2 (0×0058e000)

  
起初我在装的时候  
libasneu.so.1 => 为空  
所以  

#cp /opt/adobe/fms/libasneu.so.1 /lib/libasneu.so.1

然后

#./fmsmgr adminserver start

2.如果4个进程都跑起来了但是fms_adminConsole.swf还是连不上

那么试试看将你的防火墙关闭先

开启： service iptables start  
关闭： service iptables stop

永久性的 --

开启： chkconfig iptables on  
关闭： chkconfig iptables off

这样安全么？测试的时候可以，放到外面当然不行了

编辑防火墙配置

vi /etc/sysconfig/iptables

找到-A RH-Firewall-1-INPUT -j REJECT --reject-with icmp-host-prohibited

在其上+上

-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 1111 -j ACCEPT

-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 1935 -j ACCEPT  
  
然后/etc/rc.d/init.d/iptables restart

就ok了  

humen1 Tech