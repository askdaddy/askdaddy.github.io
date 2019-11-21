---
title: haproxy 配置
tags:
  - cdn
  - haproxy
url: 588.html
id: 588
categories:
  - CDN
date: 2013-05-04 09:24:58
---

自己的测试环境 squid listen :8081 haproxy listen :80 \[bash\] lobal maxconn 1024 #限制单个进程的最大连接数 chroot /haproxy #安装路径 uid 99 #运行用户 99==nobody gid 99 #运行组 99==nobody daemon #as 守护进程 quiet nbproc 10 #启动多少个进程 pidfile /haproxy/run.pid # pid 文件的路径 defaults log global mode http option httplog option dontlognull log 127.0.0.1 local3 info #日志级别\[err warning info debug\] retries 3 #在一个服务器上连接失败后重试次数 option redispatch #连接失败或断开后允许当前会话被重新分配 maxconn 1024 #连后端服务器的最大连接数 contimeout 100ms #连接超时 clitimeout 10000ms #客户端的连接超时 srvtimeout 10000ms #服务端的连接超时 listen cluster 0.0.0.0:80 #监听 host：port mode http #http 7层模式 balance roundrobin # 负载方式 option httpclose option forwardfor server internalweb1 127.0.0.1:8081 weight 5 #weight 权重 #check 健康检查 【我没配置】 #inter n 两次check间隔时间ms（检查粒度） #rise n 指定成功检测n次后服务可用 #fall n 指定检测n次失败后服务不可用 #maxconn n 指定最大并发连接数 \[/bash\] [参考网址](http://heylinux.com/archives/1752.html)