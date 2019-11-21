---
title: Apache Prefork和Worker模式的性能比较测试
url: 20.html
id: 20
categories:
  - 'NULL'
  - 技术杂文
date: 2009-01-09 11:22:00
tags:
---

选择prefork还是worker可以在编译时使用�with-mpm=MPM参数指定,默认为prefork,  
prefork  
prefork采用预派生子进程方式，用单独的子进程来处理 不同的请求，进程之间彼此独立。在make编译和make  
install安装后，使用httpd  
-l来确定当前使用的MPM是prefork.c。查看httpd-mpm.conf配置文件，里面包含如下默认的配置段：  
<IfModule prefork.c>  
StartServers 5  
MinSpareServers 5  
MaxSpareServers 10  
MaxClients 150  
MaxRequestsPerChild 0  
</IfModule>  
prefork 控制进程在最初建立"StartServers"个子进程后，为了满足MinSpareServers设置的需要创建一个进程，等待一秒钟，继续创建两  
个，再等待一秒钟，继续创建四个……如此按指数级增加创建的进程数，最多达到每秒32个，直到满足MinSpareServers设置的值为止。这种模式  
可以不必在请求到来时再产生新的进程，从而减小了系统开销以增加性能。MaxSpareServers设置了最大的空闲进程数，如果空闲进程数大于这个  
值，Apache会自动kill掉一些多余进程。这个值不要设得过大，但如果设的值比MinSpareServers小，Apache会自动把其调整为  
MinSpareServers+1。如果站点负载较大，可考虑同时加大MinSpareServers和MaxSpareServers。  
MaxRequestsPerChild设置的是每个子进程可处理的请求数。每个子进程在处理了"MaxRequestsPerChild"个请求后将自  
动销毁。0意味着无限，即子进程永不销毁。虽然缺省设为0可以使每个子进程处理更多的请求，但如果设成非零值也有两点重要的好处：1、可防止意外的内存泄  
漏。2、在服务器负载下降的时侯会自动减少子进程数。因此，可根据服务器的负载来调整这个值。MaxClients是这些指令中最为重要的一个，设定的是  
Apache可以同时处理的请求，是对Apache性能影响最大的参数。其缺省值150是远远不够的，如果请求总数已达到这个值（可通过ps  
-ef|grep http|wc  
-l来确认），那么后面的请求就要排队，直到某个已处理请求完毕。这就是系统资源还剩下很多而HTTP访问却很慢的主要原因。虽然理论上这个值越大，可以  
处理的请求就越多，但Apache默认的限制不能大于256。ServerLimit指令无须重编译Apache就可以加大MaxClients。  
<IfModule prefork.c>  
ServerLimit 10000  
StartServers 5  
MinSpareServers 5  
MaxSpareServers 10  
MaxClients 10000  
MaxRequestsPerChild 0  
</IfModule>

Worker  
相 对于prefork，worker全新的支持多线程和多进程混合模型的MPM。由于使用线程来处理，所以可以处理相对海量的请求，而系统资源的开销要小于  
基于进程的服务器。但是，worker也使用了多进程，每个进程又生成多个线程，以获得基于进程服务器的稳定性。在configure  
�with-mpm=worker后，进行make编译、make  
install安装。在缺省生成的httpd-mpm.conf中有以下默认配置段：  
<IfModule worker.c>  
StartServers 2  
MaxClients 150  
MinSpareThreads 25  
MaxSpareThreads 75  
ThreadsPerChild 25  
MaxRequestsPerChild 0  
</IfModule>  
Worker 由主控制进程生成"StartServers"个子进程，每个子进程中包含固定的ThreadsPerChild线程数，各个线程独立地处理请求。同样，  
为了不在请求到来时再生成线程，MinSpareThreads和MaxSpareThreads设置了最少和最多的空闲线程数；而MaxClients  
设置了同时连入的clients最大总数。如果现有子进程中的线程总数不能满足负载，控制进程将派生新的子进程。MinSpareThreads和  
MaxSpareThreads的最大缺省值分别是75和250。这两个参数对Apache的性能影响并不大，可以按照实际情况相应调节。  
ThreadsPerChild是worker  
MPM中与性能相关最密切的指令。ThreadsPerChild的最大缺省值是64，如果负载较大，64也是不够的。这时要显式使用  
ThreadLimit指令，它的最大缺省值是20000。Worker模式下所能同时处理的请求总数是由子进程总数乘以ThreadsPerChild  
值决定的，应该大于等于MaxClients。如果负载很大，现有的子进程数不能满足时，控制进程会派生新的子进程。默认最大的子进程总数是16，加大时  
也需要显式声明ServerLimit（最大值是20000）。需要注意的是，如果显式声明了ServerLimit，那么它乘以  
ThreadsPerChild的值必须大于等于MaxClients，而且MaxClients必须是ThreadsPerChild的整数倍，否则  
Apache将会自动调节到一个相应值。  
<IfModule worker.c>  
ServerLimit 25  
ThreadLimit 200  
StartServers 3  
MaxClients 2000  
MinSpareThreads 50  
MaxSpareThreads 200  
ThreadsPerChild 100  
MaxRequestsPerChild 0  
</IfModule>  
下面是利用Apache自带的测试工具ab对Server进行测试的情况(设定请求的index页面为6bytes),cpu%为cpu占用率，mem为内存使用量(M为单位)，RequestsPerSecond为每秒处理的请求数。  
1、Prefor方式  
(ServerLimit,StartServer,MinSpareServers,MaxSpareServers,MaxClients,MaxRequestPerChild)  
-n/-c(ab参数) Cpu% Mem  
Requestspersecond  
(－,5,5,10,150,0)  
100000/100 28.8 285 8434  
100000/200 29.2 304 8032  
100000/500 25.3 323 7348  
100000/1000 24.4 330 5886  
(10000,5,5,10,500,0)  
100000/100 28.7 371 8345  
100000/200 27.4 389 7929  
100000/500 24.9 417 7229  
100000/1000 23.4 437 6676  
(10000,5,5,10,1000,0)  
100000/100 28.8 408 8517  
100000/200 27.0 422 8045  
100000/500 24.2 455 7236  
100000/1000 22.5 470 6570  
(10000,5,5,10,1500,0)  
100000/100 29.6 330 8407  
100000/200 28.1 349 8014  
100000/500 26.4 380 7290  
100000/1000 24.0 400 6686  
2、Worker方式  
(ServerLimt,Threadlimt,Startservers,MaxClients,MinspareThread,MaxspareThread,ThreadperChild,MaxRequestPerChild)

-n/-c(ab参数) cpu% mem RequestsperSecond  
(50,500,5,10000,50,200,200,0)  
100000/100 18.6 188 6020  
100000/200 20.1 195 5892  
100000/500 19.8 209 5708  
100000/1000 22.2 218 6081  
(100,500,5,10000,50,200,100,0)  
100000/100 24.5 240 6919  
100000/200 23.6 247 6798  
100000/500 24.6 254 6827  
100000/1000 22.3 271 6114  
(200,500,5,10000,50,200,50,0)  
100000/100 27.3 301 7781  
100000/200 27.4 307 7789  
100000/500 26.0 320 7141  
100000/1000 21.8 344 6110  
相对来说，prefork方式速度要稍高于worker，然而它需要的cpu和memory资源也稍多于woker。

humen1 Tech![](https://blogger.googleusercontent.com/tracker/7269874978253342363-2824117072610295259?l=www.humen1.net)