---
title: SAMBA配置详解
tags:
  - linux
url: 96.html
id: 96
categories:
  - 'NULL'
date: 2008-01-17 10:23:00
---

使用 Linux 和 SAMBA替代Windows NT/2000 服务器

摘要:

这一篇文章提供了以前LinuxFocus 文章关于SAMBA用于在Unix-Windows异构网络共享资源的方案。 特别地，它集中在使用SAMBA运行Windows提供的服务。  
这不仅是因为Linux强大灵活，还更出于经济考虑的结果:

\* 极大的节省了购买Windows服务器的许可证费用。  
\* 要达到相似的性能表现，Linux比Windows使用更少的硬件资源（也就是处理器和内存了）。

  
一个运行SAMBA配置恰当的Linux服务器可以替代Windows NT/2000服务器， 它一般能共享目录, 提供活动目录服务(active directory service ,ADS) 但是它可以做为主域控制器(Primary Domain Controller, PDC), 进行 Windows 2000/NT/98/95 作为客户机的用户认证 ，共享资源（目录和打印机） 和定制用户会话。  
这篇文章主要集中到这些方面。

许多的计算机环境都以Windows 服务器提供的功能为基础，装有SAMBA的Linux 服务器会在不改变客户机的情况下，替代所有基于Windows系统提供的功能。  
以下的要讨论的步骤假定：SAMBA已经安装并且运行正确的机器将被用做服务器。读者需要 Linux和Windows服务器的基本的知识。

案例学习

考虑Linux/Samba 服务器作为主域控制器（PDC）, 每个认证过的用户进入 两种共享的目录，一个是公共空间，一个是私人空间。在这篇文章里，讨论一种进 入私人数据空间的极为常见的情况，就是每个用户有一个个人的目录。

要考虑的细节：

Linux/Samba NetBIOS 名字:SMBServer  
Windows 域名(工作组): THEDOMAIN  
每个用户的私人分区: H: (Windows) => /home/ (Linux server)  
公共分区: P: (Windows) => /home/public

  
图 1 显示了一个简单的网络示意图，客户机运行Windows系统，使用 Windows NT/2000服务器提供的资源和服务。 这个服务器能被 Linux/SAMBA服务器替代。

  
Fig. 1 � 在Windows服务器上运行的主域控制器和 文件服务器

配置

遵循以下步骤：

1) 创建要在主域服务器(Linux/Samba)待认证的用户。  
使用adduser 命令, useradd 或 userconf, 你可以使用一些用户管理的工具，也可以 是带有图形界面的(Webmin，Linuxconf，Yast等).

需要确认如果用户只进入Linux/Samba服务（如果你想）， 这就是说用户不必进入Linux命令行，这样的话只有把home目录设成/dev/null ，命令行设成/bin/false。

2) 把UNIX用户转换成Linux/Samba/Windows用户,生成smbpasswd 文件。

cat /etc/passwd | mksmbpasswd.sh > /etc/samba/smbpasswd

另一个方法是，执行一下的SAMBA命令来创建用户和定义密码：

smbadduser  
smbpasswd

这些命令和adduser与passwd一样有类似的作用。

3) 编辑SAMBA的配置文件（smb.conf）， 你要确定加入或减去下列标有comment的可选项：

netbios name = SMBServer  
workgroup = THEDOMAIN  
server string = Linux Samba NT Server  
log file = /var/log/samba/%m.log  
max log file = 0  
security = user  
encrypt password = yes  
smb password file = /etc/samba/smbpasswd  
ssl CA certificate = /usr/share/ssl/.... (cancel comment)  
socket options = (cancel comment)  
local master = yes  
preferred master = yes  
domain master = yes  
domain logons = yes  
logon script = logon.bat  
wins support = yes

注意：  
做为每一个用户的特有的登陆(login)， 需要使用"%U.bat"文件替换 原先的"登陆描述"(login script)。这样每一个用户都有一个的带有自 己用户名的"登陆描述"， %u 也是可以使用的. 如果你想定义用户属于 那个组，你可以使用 %g或%G，这些参数和其他参数的定义可以在手册 中找到。(man smb.conf)

4) 创建共享资源  
编辑smb.conf 文件 并注释所有的"共享"的例子，加入以下 的信息，如果没有必要的话，不用更改：

\[netlogon\]  
comment = Initialization Scripts  
path = /home/netlogon  
read only = yes  
guest ok = yes  
browseable = no

\[home\]  
comment = User Directory  
path = /home/%U  
browseable = yes  
writable = yes

\[public\]  
comment = Public Directory  
path = /home/public  
browseable = yes  
writable = yes  
guest ok = yes  
create mask = 0777  
force create mask = 0777

保存smb.conf 文件。

5) 你可以使用如下的命令来验证smb.conf是否正确：

testparm

这些命令分析smb.conf 文件并报告发现的错误。

6) 分别使用权限0754和0777 创建/home/netlogon 和/home/public目录。

7) 编辑logon描述文件logon.bat。  
重要提示: 使用DOS/Windows文字编辑器 （比如Notepad或Edit）来创建logon.bat文件 （所以保存的文本文件是微软兼容的形式），你也可以在Linux上做这件事但是你必须转换成正确的文本形式。 你可以使用比如 Vim的命令":set textmode"得到有微软行结尾符的文件。

net time SMBServer /y (you can also use: /yes instead of /y )  
net use H: SMBServerhome -y (you can also use: /yes or /y instead of -y )  
net use P: SMBServerpublic -y

8) 加入SMBServer信息到lmhosts文件中。  
编辑/etc/samba/lmhosts 文件后 /etc/lmhosts)文件并且 加入关于SMBServer信息的一行。

SMB服务器, 比如: [192.168.0.10](http://192.168.0.10) SMBServer

9) 重启动SAMBA的后台程序（smbd）。

service smb restart

如果在你的Linux版本中上面的命令不工作，你可以使用如下命令：  
ps -auxgx | grep smb  
kill -9  
smbd

10) 使用smbclient来验证以上的配置是正确的。

smbclient -L //SMBServer

如果"Password:"显示出来, 按"Enter" 键，服务器的共享的 资源会显示出来。

11) 使用Windows 95/98/NT 计算机在域THEDOMAIN中进行客户登陆， 使用Linux/Samba创建的用户（看步骤1和2）。

在95/98/ME中, 配置可以按照一下的顺序：

开始 => 设置 => 控制面板=> 网络 =>微软网络客户 =\> 属性。

Windows NT/2000（工作站/专业版）中也是类似的用法， 可能顺序不是一样。

单击选项"Start session in Windows NT/2000 domain" 并写下域名 THEDOMAIN (WORKGROUP)。

一个配置文件的实例

一个完整的SAMBA配置文件罗列如下，这个文件在不通的Linux分发版本中测试通过。 读者可以修改它以达到自己想要的结果。其中每条指令都被恰当的注释。

最后，给那些