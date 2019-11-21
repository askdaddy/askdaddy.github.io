---
title: FreeBSD 下安装Samba
tags:
  - unix
url: 102.html
id: 102
categories:
  - 'NULL'
date: 2007-12-25 23:48:00
---

在FreeBSD 下安装Samba 
------------------

1\. Samba 安装

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

Samba有二进制安装的版本, 也有源代码安装版本. 我用的系统是FreeBSD,

Samba的二进制安装并不支持FreeBSD. 所以, 我就选择了源代码安装方式.

我使用的samba版本是 samba-3.0.21a.tar.gz

shell> tar zxvf samba-3.0.21a.tar.gz

shell> cd samba-3.0.21a/source

shell> ./configure

shell> make

shell> make install

shell> cp ../examples/smb.conf.default /usr/local/samba/lib/smb.conf

2\. 创建用户

\-\-\-\-\-\-\-\-\-\-\-\-\-

这里我不得不说一句,目前我还没看到网上有任何一篇文章仔细地解释samba的用户关系问题!

不厚道啊~~ 我是摸索了好久才得出以下认识的:

    (1)samba用户管理使用smbpasswd和pdbedit命令

    (2)samba认证使用的用户和组首先要在本地系统中存在

    (3)samba只存储独立于本地系统的用户和口令信息,组则使用本地系统的组信息

首先在本地系统中创建用户user1和user2, 创建组group1和group2, user1属于group1,

user2属于group2.

然后再创建samba用户:

shell> /usr/local/samba/bin/smbpasswd -a user1

New SMB password:  
Retype new SMB password:

shell> /usr/local/samba/bin/smbpasswd -a user2

New SMB password:  
Retype new SMB password:

如果失败,则可能是本地系统没有事先建立同名帐号.

可以使用pdbedit -L列出现有samba用户清单, 如果清单中有新加入的用户名, 则说明用户

创建成功.

3\. 配置Samba

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

shell> vi /usr/local/samba/lib/smb.conf

下面是我实际搭建环境中的一个实例:

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

\# Samba config file created using SWAT  
\# from [10.217.15.133](http://10.217.15.133) ([10.217.15.133](http://10.217.15.133))  
\# Date: 2006/01/05 09:42:54

\[global\]  
        workgroup = MYGROUP  
        netbios name = SINA-NFS  
        server string = Sina NFS  
        log file = /usr/local/samba/var/log-%M-%I  
        max log size = 50  
        load printers = No  
        dns proxy = No

\[it\]  
        path = /data1/it  
        valid users = @group1, @group2  
        read list = @group1, @group2  
        write list = @group1, @group2

\[driver\]  
        path = /data2/driver  
        write list = @group1  
        guest ok = Yes

\[software\]  
        path = /data2/software  
        write list = @group1  
        guest ok = Yes

\[patch\]  
        path = /data2/patch  
        write list = @group1  
        guest ok = Yes

以上是通过SWAT配置后生成的最终配置文件,但实际上我手工配置时还在global部分加入了:

   security = user  
   encrypt passwords = yes  
   smb passwd file = /usr/local/samba/private/smbpasswd

那上面配置要实现的目的是:

(1)所有用户都可以看到(browseable)共享目录it,driver,software,patch;

(2)group1的用户对共享目录it,driver,software,patch有读写权限;

(3)group2的用户对共享目录it有读写权限,对共享目录driver,software,patch只读;

(4)非group1和group2的用户对共享目录driver,software,patch只读,对共享目录it无读写权限;

4.设置共享目录权限

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

shell> chmod -R 0777 /data1/it

shell> chmod -R 0777 /data2/driver

shell> chmod -R 0777 /data2/patch

shell> chmod -R 0777 /data2/software

5.启动samba

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

/usr/local/samba/sbin/smbd -D &

/usr/local/samba/sbin/nmbd -D &

6.自动运行samba

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

有两种方法:

(1)在/etc/rc.local加入以下内容:

/usr/local/samba/sbin/smbd -D &

/usr/local/samba/sbin/nmbd -D &

(2)在/etc/inetd.conf中加入以下内容:

netbios-ssn  stream  tcp  nowait       root  /usr/local/samba/sbin/smbd -D   smbd  
netbios-ns   dgram   udp  wait         root  /usr/local/samba/sbin/nmbd -D   nmbd  
swat         stream  tcp  nowait/400   root  /usr/local/samba/sbin/swat      swat  

第二种方法要保证inetd正常运行.

7.SWAT管理

\-\-\-\-\-\-\-\-\-\-\-\-\-

默认情况下SWAT已被安装.

我试过通过执行/usr/local/samba/sbin/swat启动SWAT没有成功, 只有通过inetd.conf才可以成功启动.

启动成功后可以通过[http://samba\_server\_ip:901/](http://samba_server_ip:901/)访问SWAT管理页面.

默认情况, SWAT使用本地系统的root用户作为管理帐号. 注意, 是系统用户, 不是samba的共享用户.

8.检查服务是否正常

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

通过netstat -an看到服务端口已处理监听状态:

tcp4       0      0  *.901                  *.*                    LISTEN  
tcp4       0      0  *.139                  *.*                    LISTEN  
udp4       0      0  10.0.0.38.138          *.*                     
udp4       0      0  10.0.0.38.137          *.*

udp4       0      0  *.138                  *.*

udp4       0      0  *.137                  *.*

9.小技巧

\-\-\-\-\-\-\-\-\-\-\-\-\-

(1)如何在一个共享目录中嵌入其它目录

有时我们需要使用多块磁盘, 那经常变更目录或更换磁盘非常麻烦, 我还不了解在samba中如何

使用多个磁盘支持同一共享目录. 所以, 我使用的方法是:

    *在已有共享目录中建立一个到其它磁盘的链接.*

假设我要在共享目录it下建立一个到磁盘/data3上的目录iso的链接, 那么需要进行以下操作:

shell> cd /data1/it

shell> ln -s /data3/iso iso

shell> chmod -R 0777 /data3/iso

humen1 Tech