---
title: FMS3集群配置(默认安装)
url: 59.html
id: 59
categories:
  - 'NULL'
date: 2008-06-26 10:14:00
tags:
---

在两台机器上都按照fms3  
输入相同的序列号

  
边缘服务器 [192.168.1.102](http://192.168.1.102)  
源服务器   [192.168.1.104](http://192.168.1.104)

在源服务器的放上服务器脚本无需配置

边缘服务器配置：  
/opt/adobe/fms/conf/\_defaultRoot\_/\_defaultVHost\_/Vhost.xml

找到 标签  
改为 将local改为remote

ok配置相当简单

呼叫的时候原本的uri  
rtmp://[192.168.1.104/](http://192.168.1.104/)

改为

rtmp://[192.168.1.102/?rtmp://192.168.1.104/](http://192.168.1.102/?rtmp://192.168.1.104/)  
【rtmp://边缘1?rtmp://边缘2?rtmp://边缘3?rtmp://边缘4?rtmp://源】

fms3的集群就部署好了

humen1 Tech