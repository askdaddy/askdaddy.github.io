---
title: 'CentOS官方推荐的RPMforge软件仓库安装方法[linux]'
url: 36.html
id: 36
categories:
  - 'NULL'
date: 2008-12-02 13:11:00
tags:
---

  

  

RPMForge拥有4000多种CentOS的软件包，被CentOS社区认为是最安全也是最稳定的一个软件仓库。

主页：[http://rpmforge.net/](http://rpmforge.net/)

  

1、确认系统是否安装了priority这个yum的插件，这个插件用来保证安装软件时候软件仓库先后次序，一般是默认先从官方base或者镜像安装，然后从社区用户contribute的软件中安装，再从第三方软件仓库中安装。当然这个次序可以自己更改，为了安全和稳定还是依照这个次序吧....

  

#yum install yum-priorities

  

安装完以后查看 /etc/yum/pluginconf.d/priorities.conf 文件，确认文件中有这一行

\[main\]

enabled=1

  

  

2、现在就可以手动编辑 /etc/yum.repos.d/ 目录中后缀为.repos的文件来设置软件仓库的先后次序（感觉我这个翻译不是很适当，priority主要还是个权限问题，但一时找不到更好的词，就这样吧）....

  

priority=N(N是整数，范围从1-99)

  

官方推荐配置是

\[base\], \[addons\], \[updates\], \[extras\] ... priority=1 

\[centosplus\],\[contrib\] ... priority=2

Third Party Repos such as rpmforge ... priority=N  (where N is > 10 and based on your preference)

  

3、现在开始安装rpmforge的软件仓库

a 先下载rpmforge的安装包

      i386 [http://apt.sw.be/redhat/el5/en/i386/RPMS.dag/rpmforge-release-0.3.6-1.el5.rf.i386.rpm](http://apt.sw.be/redhat/el5/en/i386/RPMS.dag/rpmforge-release-0.3.6-1.el5.rf.i386.rpm)

  

      x86_64 [http://apt.sw.be/redhat/el5/en/x86\_64/RPMS.dag/rpmforge-release-0.3.6-1.el5.rf.x86\_64.rpm](http://apt.sw.be/redhat/el5/en/x86_64/RPMS.dag/rpmforge-release-0.3.6-1.el5.rf.x86_64.rpm)

*不知道什么架构的用 uname -i 命令查看

b 安装DAG的PGP Key

rpm --import [http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt](http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt)

  

c 验证下载包的完整性

rpm -K rpmforge-release-0.3.6-1.el5.rf.*.rpm

  

d 安装包

rpm -i rpmforge-release-0.3.6-1.el5.rf.*.rpm

  

e 更改 /etc/yum.repos.d/rpmforge.repo 配置文件，就是添加

priority=3（或者[1.2.4.](http://1.2.4.)...）这一句

  

f 现在就可以使用rpmforge这个软件仓库了....

  

humen1 Tech