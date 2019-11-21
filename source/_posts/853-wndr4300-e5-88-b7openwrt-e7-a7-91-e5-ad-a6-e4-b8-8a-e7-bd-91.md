---
title: wndr4300 刷openwrt 科学上网
tags:
  - linux
  - openwrt
  - 路由
url: 853.html
id: 853
categories:
  - network
date: 2015-07-23 19:51:14
---

刷机 基础配置
-------

[参考文件入口](https://cokebar.info/archives/664) [需要的刷机文件@百度网盘](http://pan.baidu.com/s/1dDrWA4L) [shadowsocks-spec](http://sourceforge.net/projects/openwrt-dist/files/shadowsocks-libev/) [chinadns-openwrt](http://sourceforge.net/projects/openwrt-dist/files/chinadns/) [luci-app-shadowsocks](http://sourceforge.net/projects/openwrt-dist/files/luci-app/shadowsocks-spec/) [luci-app-chinadns](http://sourceforge.net/projects/openwrt-dist/files/luci-app/chinadns/)

初始安装软件
------

@win \[code lang=bash\] <br />C:\\Users\\seven\\Documents\\wdnr4300>pscp.exe *.ipk root@192.168.1.1:/opt/ 2015/07/23 14:38 27,161 ChinaDNS\_1.3.1-1\_ar71xx.ipk 2015/07/23 14:38 2,592 luci-app-chinadns\_1.3.1-1\_all.ipk 2015/07/23 14:38 3,131 luci-app-shadowsocks-spec\_1.3.2-1\_all.ipk 2015/07/23 14:38 117,469 shadowsocks-libev-spec\_2.2.2-1\_ar71xx.ipk \[/code\] @4300 \[code lang=bash\] # opkg install ip ipset libopenssl resolveip iptables-mod-tproxy # cd /opt # opkg install ./*.ipk \[/code\] 问题： \[code lang=text\] C:\\Users\\seven\\Documents\\wdnr4300>pscp.exe *.ipk root@192.168.1.1:/opt/ root@192.168.1.1's password: ash: /usr/libexec/sftp-server: not found Fatal: Received unexpected end-of-file from server \[/code\] 解决： \[code lang=text\] # opkg update # opkg install openssh-sftp-server \[/code\] **修改4300 LAN IP 192.168.7.1**

DNS
---

`#vim /etc/config/sec_resolv.conf` \[code lang=bash\] nameserver 8.8.8.8 nameserver 8.8.4.4 nameserver 114.114.114.114 \[/code\]

无线和有线设置
-------

忽略了，直接在web界面设置就好主要是设密码什么的

pdnsd搭建DNS服务器@centos 服务器
------------------------

从 http://members.home.nl/p.a.rombouts/pdnsd/dl.html 下载pdnsd最新的rpm包 然后 yum localinstall pdnsd-x.x.x-par\_sl6.x86\_64.rpm 配置见： https://cokebar.info/archives/720 http://leeraw.com/?p=3621

搭建shadowsocks服务@centos 服务器
--------------------------

1.  先安装git
2.  从github上拉源码 https://github.com/shadowsocks/shadowsocks-libev
3.  cd shadowsocks-libev
4.  ./configure
5.  make && make install
6.  启动 \> nohup /usr/local/bin/ss-server -s SERVER\_IP -p SERVER\_PORT -k PASSWD -m aes-256-cfb & > 将上面的启动命令加到rc.local开机自启
7.  配置

进阶
--

https://cokebar.info/archives/850

交换机截图
-----

[![chinaDNS](/uploads/2015/07/OpenWrt_-_ChinaDNS_-_LuCI-300x166.png)](/uploads/2015/07/OpenWrt_-_ChinaDNS_-_LuCI.png) [![shadowsocks](/uploads/2015/07/OpenWrt_-_ShadowSocks_-_LuCI-170x300.png)](/uploads/2015/07/OpenWrt_-_ShadowSocks_-_LuCI.png) [![dhcp-dns](/uploads/2015/07/OpenWrt_-_DHCP_and_DNS_-_LuCI-300x223.png)](/uploads/2015/07/OpenWrt_-_DHCP_and_DNS_-_LuCI.png) [![dncp-dns](/uploads/2015/07/OpenWrt_-_DHCP_and_DNS_-_LuCI1-300x160.png)](/uploads/2015/07/OpenWrt_-_DHCP_and_DNS_-_LuCI1.png)