---
title: Red Hat Linux配置文件一览
tags:
  - linux
url: 111.html
id: 111
categories:
  - 'NULL'
date: 2008-01-25 10:57:00
---

  
配置文件是Red Hat Linux管理的一个主要内容.为特定计算机进行的设置,包括用户帐号,网络地址或GUI属性,都保存在纯文本中.  
　　一般情况下,Red Hat Linux系统的配置文件被保存在几个地方,下面是几个主要的地方:  
　　  
　　1.$HOME:所有的用户都把信息保存在他们的主目录下,该目录可指导他们的登录帐号操作.大多数的配置文件都用圆点(.)开始,因次使用标准的ls命令(需要键入ls -a查看它), 配置文件不出现在用户的目录中.有定义用户shell行为,桌面外观以及文本编辑器使用的选项的圆点文件,甚至有为每个用户配置网络权限的文件(如.rhosts).  
　　  
　　2./etc:这个地方包括许多最基本的Red Hat Linux系统配置文件,这些文件包括:  
　　  
　　(1)aliases:可以包含由Red Hat Linux邮件服务使用的分布表.  
　　(2)bashrc:为bash shell用户设置系统默认值(默认情况下,它可以设置shell提示符,包括当前的用户名,主机名以及当前的目录).  
　　(3)crontab:为运行自动任务设置cron环境和次数.  
　　(4)csh.cshrc(或cshrc):为csh(C shell)用户设置系统默认值.  
　　(5)exports:包含一些本地目录列表,远程计算机可以使用Network File System(网络文件系统,简称NFS)共享这些目录.  
　　(6)fdprm:设置供通用软盘格式使用的参数.  
　　(7)fstab:识别共用存储媒体用的设备(硬盘,软盘以及光驱)以 及在Linux系统中安装它们的位置.使用mount命令选择要安装哪个文件系统.  
　　(8)gettydefs:包含终端设备(调制解调器,终端以及在终端设备上的远程登录)使用的线行定义.  
　　(9)group:识别定义在系统上的分组名以及分组ID(GID).Linux中的分组权限由与每个文件以及目录关联的rwx(读,写,执行)三个设置中的第二个来定义.  
　　(10)host.conf:设置在TCP/IP网络(如 Internet)上用于搜索域名(如 [redhat.com](http://redhat.com))的位置.默认情况下,搜索本地主文件,然后是resolv.conf中的名字服务器项.  
　　(11)hosts:包含可以从计算机中搜索到的IP地址和主机名(通常该文件仅用于保存LAN活更大的私人网络上的计算机名).  
　　(12)host.allow:列出允许在本地计算机上使用TCP/IP服务的主计算机.  
　　(13)host.deny:列出不允许本地计算机上使用TCP/IP服务的主计算机.  
　　(14)xinetd.conf:包含daemon过程中用到的一些简单配置信息.单个服务器的信息都会被放在/etc/xinetd.d目录中.  
　　(15)info-dir:包含info命令可用信息的标题.  
　　(16)inittab:包含确认哪些程序启动和结束的信息.  
　　(17)issue:包含一些登录信息行,这些登录信息行是在终端准备好允许你从本地终端或也文本模式下的控制台中登录到linux时所显示的.  
　　(18)issue.net:包含用户使用telnet服务从网络的计算机上登录到Linux系统上所显示出的登录信息行.  
　　(19)lilo.conf:设置linux启动加载器(lilo)使用的各种参数来启动Linux系统.  
　　(20)mail.rc:设置与使用邮件相关的系统参数.  
　　(21)man.config:man命令用来确认man页面位置的默认路径的文件.  
　　(22)mtab:包含当前安装的文件系统列表.  
　　(23)passwd:为系统的所有合法用户保存帐号信息;也包含其他信息,如主目录和默认shell.  
　　(24)profile:设置所有用户使用的系统环境和启动程序,当有用户登录时读取这个文件.  
　　(25)printcap:包含打印机配置的定义信息.  
　　(26)protocols:设置各种Internet服务用的协议编号和名字.  
　　(27)redhat-release:包含识别当前Red Hat 版本号的字符串.  
　　(28)resolv.conf:识别DNS名字服务器计算机的位置,TCP/IP用该计算机把Internet host.domain名转换成IP地址.  
　　(29)rpc:定义远程过程调用名和编号.  
　　(30)rpmfind:包含rpmfind命令所使用配置信息,rpmfind在Internet上搜索RPM软件包的.  
　　(31)services:定义TCP/IP服务以及它们的端口分配.  
　　(32)shadow:包含定义在passwd文件中的加密口令.  
　　(33)shells:列出可用在系统上的shell命令行解释器(bash,sh,csh等).  
　　(34)syslog.conf:定义daemon产生的登录信息以及它们被保存在什么文件中.(一般说来,登录信息被保存在/var/log目录下的文件中).  
　　(35)termcap:列出供字符终端使用的定义,这样基于字符的应用程序就可以知道给出的终端支持哪些特性.  
　　(36)php.ini:Linux系统上的PHP配置文件.  
　　(37)ftpaccess:wu-ftp服务器的访问配置文件.  
　　(38)vsftpd.conf:vsftp服务的配置文件.  
　　3./etc/X11:包含子目录,而每个子目录又包含RedHat Linux上可用的X以及不同X Window管理程序使用的系统配置文件.XF86Config文件以及配置包含使用xdm以及xinit启动X的文件目录.  
　　  
　　4./etc/corn*:这是一组包含定义crond工具运行应用程序文件的目录,运行按每天,每小时,每月和每周来安排.  
　　  
　　5./etc/default:包含为各种工具设置默认值的文件.例如,useradd命令所用的文件定义了在创建新用户帐号时说用到的默认分组数,主目录,口令截止日期,shell以及框架目录(/etc/skel).  
　　  
　　6./etc/httpd:包含用于配置Apache服务器的文件.  
　　  
　　7./etc/init.d:包含运行脚本的永久拷贝.这些脚本与/etc/rc?.d目录中的文件链接.  
　　  
　　8./etc/pcmcia:包含使你为计算机配置各种PCMCIA卡的配置文件.  
　　  
　　9./etc/ppp:包含用于设置Point-to-Point协议的配置文件(以便使你的计算机能用拨号方式上网).  
　　  
　　10./etc/rc?.d:包含几个子目录,每个子目录又包含在系统启动,关闭以及系统状态修改期间直接使程序启动和停止的配置文件.  
　　  
　　11./etc/security:包含设置计算机使用的各种默认安全条件的文件.  
　　  
　　12./etc/skel:当某个用户增加到系统中时,包含在该目录下的任何文件就被自动复制到该用户的主目录中.  
　　  
　　13./etc/xinetd.d:包含一组文件,每个文件定义xinetd守护进程的特殊端口等待的网络服务程序.当xinetd守护进程过程接受请求服务程序时,它使用这些文件的信息来确定用来处理请求的守护程序.  

humen1 Tech