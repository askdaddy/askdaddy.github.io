---
title: 基于Apache mod_proxy的反向代理缓存加速实现
tags:
  - unix
url: 94.html
id: 94
categories:
  - 'NULL'
date: 2008-01-11 16:08:00
---

　　Apache包含了mod_proxy模块，可以用来实现代理[服务器](http://www.bitscn.com/server/)，针对后台[服务器](http://www.bitscn.com/server/)的反向加速  
　　安装apache 1.3.x 编译时：  
　　--enable-shared=max --enable-module=most  
　　注：Apache 2.x中mod\_proxy已经被分离成mod\_proxy和mod\_cache：同时mod\_cache有基于文件和基于内存的不同实现  
　　创建/var/www/proxy，设置apache服务所用户可写  
　　mod_proxy配置样例：反相代理缓存＋缓存  
　　架设前台的www.example.com反向代理后台的www.backend.com的8080端口服务。  
　　修改：httpd.conf  
　　  
　　ServerName [www.example.com](http://www.example.com)  
　　ServerAdmin [admin@example.com](mailto:admin@example.com)  
　　# reverse proxy setting  
　　ProxyPass / [http://www.backend.com:8080/](http://www.backend.com:8080/)  
　　ProxyPassReverse / [http://www.backend.com:8080/](http://www.backend.com:8080/)  
　　# cache dir root  
　　CacheRoot "/var/www/proxy"  
　　# max cache storage  
　　CacheSize 50000000  
　　# hour: every 4 hour  
　　CacheGcInterval 4 bitsCN_com  
　　# max page expire time: hour  
　　CacheMaxExpire 240  
　　# Expire time = (now - last_modified) * CacheLastModifiedFactor  
　　CacheLastModifiedFactor 0.1  
　　# defalt expire tag: hour  
　　CacheDefaultExpire 1  
　　# force complete after precent of content retrived: 60-90%  
　　CacheForceCompletion 80  
　　CustomLog /usr/local/apache/logs/dev\_access\_log combined  
　　  
　　  
　　**基于Squid的反向代理加速实现**  
　　Squid是一个更专用的代理[服务器](http://www.bitscn.com/server/)，性能和效率会比Apache的mod_proxy高很多。  
　　如果需要combined格式日志补丁：  
　　 [http://www.squid-cache.org/mail-archive/squid-dev/200301/0164.html](http://www.squid-cache.org/mail-archive/squid-dev/200301/0164.html)  
　　squid的编译：  
　　./configure --enable-useragent-log　--enable-referer-log --enable-default-err-language=Simplify\_Chinese --enable-err-languages="Simplify\_Chinese English" --disable-internal-dns　  
　　make  
　　#make install  
　　#cd /usr/local/squid  
　　make dir cache  
　　chown squid.squid *  
　　vi /usr/local/squid/etc/squid.conf 中国网管论坛  
　　在/etc/hosts中：加入内部的DNS解析，比如：  
　　 [192.168.0.4](http://192.168.0.4) \[url\]www.chedong.com\[/url\]  
　　[192.168.0.4](http://192.168.0.4) [news.chedong.com](http://news.chedong.com)  
　　[192.168.0.3](http://192.168.0.3) [bbs.chedong.com](http://bbs.chedong.com)  
　　---------------------cut here----------------------------------  
　　# visible name  
　　visible_hostname [cache.example.com](http://cache.example.com)  
　　# cache config: space use 1G and memory use 256M  
　　cache_dir ufs /usr/local/squid/cache 1024 16 256  
　　cache_mem 256 MB  
　　cache\_effective\_user squid  
　　cache\_effective\_group squid  
　　  
　　http_port 80  
　　httpd\_accel\_host virtual  
　　httpd\_accel\_single_host off  
　　httpd\_accel\_port 80  
　　httpd\_accel\_uses\_host\_header on  
　　httpd\_accel\_with_proxy on  
　　# accelerater my domain only  
　　acl acceleratedHostA dstdomain .example1.com  
　　acl acceleratedHostB dstdomain .example2.com  
　　acl acceleratedHostC dstdomain .example3.com  
　　# accelerater http protocol on port 80  
　　acl acceleratedProtocol protocol HTTP  
　　acl acceleratedPort port 80  
　　# access arc 中国网管联盟  
　　acl all src [0.0.0.0/0.0.0.0](http://0.0.0.0/0.0.0.0)  
　　# Allow requests when they are to the accelerated machine AND to the  
　　# right port with right protocol  
　　http_access allow acceleratedProtocol acceleratedPort acceleratedHostA  
　　http_access allow acceleratedProtocol acceleratedPort acceleratedHostB  
　　http_access allow acceleratedProtocol acceleratedPort acceleratedHostC  
　　# logging  
　　emulate\_httpd\_log on  
　　cache\_store\_log none  
　　# manager  
　　acl manager proto cache_object  
　　http_access allow manager all  
　　cachemgr_passwd pass all  
　　  
　　----------------------cut here---------------------------------  
　　创建缓存目录：  
　　/usr/local/squid/sbin/squid -z  
　　启动squid  
　　/usr/local/squid/sbin/squid  
　　停止squid：  
　　/usr/local/squid/sbin/squid -k shutdown  
　　启用新配置：  
　　/usr/local/squid/sbin/squid -k reconfig  
　　通过crontab每天0点截断/轮循日志：  
　　0 0 * * * (/usr/local/squid/sbin/squid -k rotate)  
　　  
　　**附：SQUID性能测试试验**

[bitscn.com](http://bitscn.com)

  
　　phpMan.php是一个基于php的man page server，每个man  
　　page需要调用后台的man命令和很多页面格式化工具，系统负载比较高，提供了Cache  
　　Friendly的URL，以下是针对同样的页面的性能测试资料：  
　　测试环境：Redhat 8 on Cyrix 266 / 192M Mem  
　　测试程序：使用apache的ab(apache benchmark)：  
　　测试条件：请求50次，并发50个连接  
　　测试项目：直接通过apache 1.3 (80端口) vs squid 2.5(8000端口：加速80端口)  
　　  
　　测试1：无CACHE的80端口动态输出：  
　　ab -n 100 -c 10 \[url\]http://www.chedong.com:81/phpMan.php/man/kill/1\[/url\]  
　　This is ApacheBench, Version 1.3d <$Revision: 1.2 $> apache-1.3  
　　Copyright (c) 1996 Adam Twiss, Zeus Technology Ltd,  
　　\[url\]http://www.zeustech.net/\[/url\]  
　　Copyright (c) 1998-2001 The Apache Group, \[url\]http://www.apache.org/\[/url\]  
　　  
　　Benchmarking localhost (be patient).....done  
　　Server Software:　　　  
　　Apache/1.3.23　　　　　　　　　　　　　　　　　　  
　　Server Hostname:　　　　localhost  
　　Server  
　　Port:　　　　　 BBS.bitsCN.com网管论坛  
　　80  
　　  
　　Document Path:　　　　  
　　/phpMan.php/man/kill/1  
　　Document Length:　　　　4655 bytes  
　　  
　　Concurrency Level:　　　5  
　　Time taken for tests:　 63.164 seconds  
　　Complete requests:　　　50  
　　Failed requests:　　　　0  
　　Broken pipe errors:　　 0  
　　Total transferred:　　　245900 bytes  
　　HTML transferred:　　　 232750 bytes  
　　Requests per second:　　0.79 \[#/sec\] (mean)  
　　Time per request:　　　 6316.40 \[ms\]  
　　(mean)  
　　Time per request:　　　 1263.28 \[ms\]  
　　(mean, across all concurrent requests)  
　　Transfer rate:　　　　  
　　3.89 \[Kbytes/sec\] received  
　　  
　　Connnection Times (ms)  
　　　　　　　　  
　　min　mean\[+/-sd\] median　 max  
　　Connect:　　　　0　  
　　29　106.1　　　0　 553  
　　Processing:　2942　6016  
　　1845.4　 6227 10796  
　　  
　　Waiting:　　  
　　2941　5999 1850.7　 6226 10795  
　　  
　　Total:　　　  
　　2942　6045 1825.9　 6227 10796  
　　  
　　Percentage of the requests served within a certain time (ms)

bitsCN.Com

  
　　　50%　 6227  
　　　66%　 706 9  
　　　75%　 7190  
　　　80%　 7474  
　　　90%　 8195  
　　　95%　 8898  
　　　98%　 9721  
　　　99%　10796  
　　100%　10796 (last request)  
　　  
　　测试2：SQUID缓存输出  
　　/home/apache/bin/ab -n50 -c5  
　　"[http://localhost:8000/phpMan.php/man/kill/1](http://localhost:8000/phpMan.php/man/kill/1)"  
　　This is ApacheBench, Version 1.3d <$Revision: 1.2 $> apache-1.3  
　　Copyright (c) 1996 Adam Twiss, Zeus Technology Ltd,  
　　\[url\]http://www.zeustech.net/\[/url\]  
　　Copyright (c) 1998-2001 The Apache Group, \[url\]http://www.apache.org/\[/url\]  
　　  
　　Benchmarking localhost (be patient).....done  
　　Server Software:　　　  
　　Apache/1.3.23　　　　　　　　　　　　　　　　　　  
　　Server Hostname:　　　　localhost  
　　Server  
　　Port:　　　　　  
　　8000  
　　  
　　Document Path:　　　　  
　　/phpMan.php/man/kill/1  
　　Document Length:　　　　4655 bytes  
　　  
　　Concurrency Level:　　　5  
　　Time taken for tests:　 4.265 seconds  
　　Complete requests:　　　50

bitsCN.nET中国网管博客

  
　　Failed requests:　　　　0  
　　Broken pipe errors:　　 0  
　　Total transferred:　　　248043 bytes  
　　HTML transferred:　　　 232750 bytes  
　　Requests per second:　　11.72 \[#/sec\] (mean)  
　　Time per request:　　　 426.50 \[ms\] (mean)  
　　Time per request:　　　 85.30 \[ms\] (mean,  
　　across all concurrent requests)  
　　Transfer rate:　　　　  
　　58.16 \[Kbytes/sec\] received  
　　  
　　Connnection Times (ms)  
　　　　　　　　  
　　min　mean\[+/-sd\] median　 max  
　　Connect:　　　  
　　0　　 1　  
　　9.5　　　0　　68  
　　Processing:　　  
　　7　　83　537.4　　  
　　7　3808  
　　  
　　Waiting:　　　  
　　5　　81　529.1　　  
　　6　3748  
　　  
　　Total:　　　　  
　　7　　84　547.0　　  
　　7　3876  
　　  
　　Perce  

humen1 Tech