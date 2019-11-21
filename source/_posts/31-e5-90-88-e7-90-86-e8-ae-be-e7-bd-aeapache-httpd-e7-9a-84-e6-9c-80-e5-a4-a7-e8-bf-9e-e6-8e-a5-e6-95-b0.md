---
title: 合理设置apache httpd的最大连接数
url: 31.html
id: 31
categories:
  - 'NULL'
date: 2008-12-06 01:42:00
tags:
---

手头有一个网站在线人数增多，访问时很慢。初步认为是服务器资源不足了，但经反复测试，一旦连接上，不断点击同一个页面上不同的链接，都能迅速打开，这种现象就是说明apache最大连接数已经满了，新的访客只能排队等待有空闲的链接，而如果一旦连接上，在keeyalive  
的存活时间内（KeepAliveTimeout，默认5秒）都不用重新打开连接，因此解决的方法就是加大apache的最大连接数。

1.在哪里设置？

服务器的为FreeBSD 6.2 ，apache 2.24，使用默认配置（FreeBSD 默认不加载自定义MPM配置），默认最大连接数是250

在/usr/local/etc/apache22/httpd.conf中加载MPM配置（去掉前面的注释）：  
\# Server-pool management (MPM specific)  
Include etc/apache22/extra/httpd-mpm.conf

可见的MPM配置在/usr/local/etc/apache22/extra/httpd-mpm.conf，但里面根据httpd的工作模式分了很多块，哪一部才是当前httpd的工作模式呢？可通过执行  
apachectl -l 来查看：  
Compiled in modules:  
core.c  
prefork.c  
http_core.c  
mod_so.c

看到prefork 字眼，因此可见当前httpd应该是工作在prefork模式，prefork模式的默认配置是：  
  
StartServers 5  
MinSpareServers 5  
MaxSpareServers 10  
MaxClients 150  
MaxRequestsPerChild 0  

2.要加到多少？

连接数理论上当然是支持越大越好，但要在服务器的能力范围内，这跟服务器的CPU、内存、带宽等都有关系。

查看当前的连接数可以用：  
ps aux | grep httpd | wc -l

或：  
pgrep httpd|wc -l

计算httpd占用内存的平均数:  
ps aux|grep -v grep|awk '/httpd/{sum+=$6;n++};END{print sum/n}'

由于基本都是静态页面，CPU消耗很低，每进程占用内存也不算多，大约200K。

服务器内存有2G，除去常规启动的服务大约需要500M（保守估计），还剩1.5G可用，那么理论上可以支持1.5\*1024\*1024*1024/200000  
= 8053.06368

约8K个进程，支持2W人同时访问应该是没有问题的（能保证其中8K的人访问很快，其他的可能需要等待1、2秒才能连上，而一旦连上就会很流畅）

控制最大连接数的MaxClients ，因此可以尝试配置为：  
  
StartServers 5  
MinSpareServers 5  
MaxSpareServers 10  
ServerLimit 5500  
MaxClients 5000  
MaxRequestsPerChild 100  

注意，MaxClients默认最大为250，若要超过这个值就要显式设置ServerLimit，且ServerLimit要放在MaxClients之前，值要不小于MaxClients，不然重启httpd时会有提示。

重启httpd后，通过反复执行pgrep httpd|wc -l  
来观察连接数，可以看到连接数在达到MaxClients的设值后不再增加，但此时访问网站也很流畅，那就不用贪心再设置更高的值了，不然以后如果网站访问突增不小心就会耗光服务器内存，可根据以后访问压力趋势及内存的占用变化再逐渐调整，直到找到一个最优的设置值。

(MaxRequestsPerChild不能设置为0，可能会因内存泄露导致服务器崩溃）

更佳最大值计算的公式：

apache\_max\_process\_with\_good\_perfermance < (total\_hardware_memory /  
apache\_memory\_per_process ) * 2  
apache\_max\_process = apache\_max\_process\_with\_good_perfermance * 1.5

参考：

apache的参数设置

Apache 2.0性能优化―MPM的选择与配置

如何避免apache的httpd进程占用比较多的内存

对apache中并发控制参数prefork理解和调优

附：

实时检测HTTPD连接数：  
watch -n 1 -d "pgrep httpd|wc -l"

humen1 Tech