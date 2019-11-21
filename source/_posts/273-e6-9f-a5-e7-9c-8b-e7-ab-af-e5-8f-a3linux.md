---
title: 查看端口linux
url: 273.html
id: 273
categories:
  - linux桌面
date: 2009-11-02 14:41:54
tags:
---

netstat -ltn 查看linux的端口使用情况 netstat -a 查看所有的服务端口 netstat -ap 查看所有的服务端口并显示对应的服务程序名 nmap ＜扫描类型＞＜扫描参数＞ 例如： nmap localhost nmap -p 1024-65535 localhost nmap -PT 192.168.1.127-245 当我们使用　netstat -apn　查看网络连接的时候，会发现很多类似下面的内容： Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name tcp 0 52 218.104.81.152:7710 211.100.39.250:29488 ESTABLISHED 6111/1 显示这台服务器开放了7710端口，那么这个端口属于哪个程序呢？我们可以使用　lsof -i :7710　命令来查询： COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME sshd 1990 root 3u IPv4 4836 TCP *:7710 (LISTEN) 这样，我们就知道了7710端口是属于sshd程序的。