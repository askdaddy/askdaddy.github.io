---
title: 'FreeBSD 利用 ports 安装与配置 apache,mysql,php'
tags:
  - unix
url: 145.html
id: 145
categories:
  - 'NULL'
date: 2007-11-20 01:52:00
---

首先申明,本帖非原创,但也不是转帖,是本人结合网络搜集的资料与自己实际安装操作过程中总结所得.那么就让我代表广大爱好者向那些站在我们脚下的巨人以及那些能抽出时间为我们写总结的人们致敬吧,因为在本人实践中深切地体会到他们的伟大与能够在百忙与他人分享经验的难能可贵.本帖适合新手或安装过程中出现同类问题的同志们参考,高人可以跳过了;但若能留下指点,自是不胜感激了.  
  
众所周知,FreeBSD 提供了软件的 ports 安装方式, 可以很方便的定制安装所需要的应用软件.当我们装好系统之后,当然首先想到是配置 web 服务器,FreeBSD 默认标准安装并没有安装 apache,mysql 和 php,所以就要亲自动手安装了.ports 安装方式的好处在于,不会像 LINUX 那样,由于一个依懒包或者库文件而导至不得不到处找依懒包或库文件,下载下来全部装好再来装需要安装的软件;因为它会自动下载并安装依懒包或库文件,当然也不是每次都成功的,毕竟每个人遇到的错误可能是千奇百怪的.尽管网络上关于这方面的东西一搜一大堆 ,但个人认为好多都只是概念性的,但手册毕竟不是万能的;所以本人结合网摘与自己在安装过程遇的问题以及对问题的分析与解决来清晰的描述整个安装过程.  
  
测试机环境:%uname -aFreeBSD [http://www.myfreebsd.cn/6.2-RELEASE](http://www.myfreebsd.cn/6.2-RELEASE) FreeBSD 6.2-RELEASE #0: Fri Jan 11 11:11:11 UTC 2007 [root@dessler.cse.buffalo.edu:/usr/obj/usr/src/sys/GENERIC](mailto:root@dessler.cse.buffalo.edu:/usr/obj/usr/src/sys/GENERIC) i386  
  
言归正传(安装系统不在讨论之列),开始我们的令人兴奋不已的征程吧.  
  
1.apache 的安装与配置apache 给人感觉不光是稳定,还有亲切.之前偶在 RedHat 下手工编译安装过,相当顺利.这次用 ports 安装,同样的顺畅.  
  
%whereis apache22apache22: /usr/ports/www/apache22 %cd /usr/ports/www/apache22%su /*取得管理员权限*/Password:www#make WITH\_MPM=worker WITHOUT\_IPV6=yes WITH\_THREADS=yes WITHOUT\_SSL=yes install clean  
  
上面是手工指定编译选项,其实也可用以下命令来通过一个简易图形化界面选择编译选项:www# make config选择好选项 OK ,然后再www# make install clean  
  
现在来配置 apache.www# cd /usr/local/etc/apache22/ /\*apache 配置文件的目录\*/www# cp httpd.conf httpd.conf.bak /*备份文件,以防不测*/www# vi httpd.conf /*编辑配置文件*/ 以下有改动的地方,当然您要是对 apache 相当熟悉了,可以略过了.(比如默认的服务器目录是 /usr/local/www/apache22/data ,可以根据需要设置.相关的配置文件忒多了.只要记得对应修改就行了.)...#管理员的电子邮箱;ServerAdmin [hy0kle@gmail.com](mailto:hy0kle@gmail.com)...#服务的名称,若没有 DNS 域名最写作主机的 IP;ServerName 192.168.0.226:80...#反正装了 PHP 后要回来设置的,不如一次性写好了.^_^添加对 PHP 的支持;偶当时少写了一个 d ,导至 apache 无法解析 PHP 文件,提示要下载文件;网有网友少写 / ;小小的疏忽造成的后果是花在量时间排错; DirectoryIndex index.html index.php...AddType application/x-gzip .gz .tgz AddType application/x-httpd-php .phpAddType application/x-httpd-php-source .phps...  
  
设置为开机自动运行.www# vi /etc/rc.conf#添加下面这句后保存退出;apache22_enable="YES"  
  
启动 apache.www# cd /usr/local/etc/apche22/rc.d/www# ./apache22 start  
  
Now,激动人心的时间到了,打开浏览器,输入 [http://127.0.0.1/](http://127.0.0.1/) 或 [http://localhost](http://localhost/) 回车.如果看到大大的"It works!"字样,那么恭喜了,apache 安装成功了.  
  
2.安装 mysqlmysql 对我来说有阴影.大四的时候,我一同学在 FreeBSD 下安装 mysql 的次数绝对不下于我在 BSD 下安装五笔\[scim\]所尝试的次数(几乎方试遍了我所能找到的方法,要不是爱迪生的精神支持着我,怕就放弃了,只不过他在发明,我在发现.最终还是尝到了成功的喜悦).故安装的时候并没有"吊以轻心".但是安装过程还是出了问题,出错信息当时忘了记录了,大致意思是 mysql-client 已经存在,但版本不一致, 无法安装.因为之前我安装过 KDE 桌面,而 mysql-client-5.0 作为一个依懒包已经安装上了.于是为为防止强制安装造成无法使用,而且最新版本不一定就好于旧版本(有点吃不到葡萄说葡萄酸的嫌疑^*^),所以我退而求其次了,没有装 5.1 ,改装 5.0 了.  
  
%cd /usr/ports/databases/mysql50-server/%suPassword:www# make WITH\_CHARSET=gbk WITH\_XCHARSET=all WITH\_PROC\_SCOPE\_PTH=yes BUILD\_OPTIMIZED=yes BUILD\_STATIC=yes SKIP\_DNS\_CHECK=yes WITHOUT\_INNODB=yes install clean 同样, mysql 也有简易图形化编译选项设置;www# make config选择好选项 OK ,然后再www# make install clean  
  
等待一会儿了...如果没有报错回到提示符,那就说明是好消息了,恭喜! mysql 也安装成功了,下面就设置它也为开机启动吧. www# rehash /*刷新一下系统*/www# vi /etc/rc.conf#添加下面的选项后保存退出;mysql_enable="YES"  
  
OK,来启动 mysql 吧.www# cd /usr/local/etc/rc.d/wwww# ./mysql-server start如果不出意外,现在 mysql 已经启动了,那么就怀着得意的心情测试一下吧:www# mysql理论上会出现 mysql 的提示符.:)  
  
3.安装 phpcome on.当初以为 php 应该不会再有什么问题了吧,可结果装了两次才算完全成功.第一次安装时 php 的扩展选项不怎么搞的没有编译进去,运行 phpMyAdmi 时报错.打印出 phpinfo 和查看 apache 配置文件时才发现, apache 根本就没有加载 php 扩展模块.于是只好卸载了重装了一遍 php.如果遇到无法卸载,想要强制重新安装,可以用以下命令:# make install FORCE\_PKG\_REGISTER="yes"  
  
OK,开始吧.%cd /usr/ports/lang/php5%suPassword:www# make config#记得一定要选中 APACHE22 ,否则 apache 不认 php 文件,会提示你让你下载文件. OK www# make install clean  
  
又是等待...如果无报错,回到提示符时,则 php 已经安装了,但是还没有扩展库.  
  
www# rehashwww# cd /usr/ports/lang/php5-extensionswww# make config/* php 的扩展库,如 GD,FTP,ZLIB,SESSION,PDF,MYSQL,HASH等等了,按需要定制吧. OK */www# make install clean  
  
如果不出什么意外,就等着收获成功的喜悦吧.不过,现在还不算完.  
  
www# rehash www# cd /usr/local/etc/rc.d/www# ./apache22 restartwww# cd /usr/local/etc/www# cp php.ini-dist php.ini www# vi php.ini/*配置 php.ini,想必到这儿所有都已经不成问题了.还是那句话,按需配置吧;保存并退出.*/...safe\_mode\_gid = Off...www# rehashwww# cd /usr/local/etc/rc.d/www# ./apache22 restart

humen1 Tech