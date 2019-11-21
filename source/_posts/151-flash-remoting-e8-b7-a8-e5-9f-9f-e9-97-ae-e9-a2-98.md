---
title: flash remoting 跨域问题
tags:
  - flash
url: 151.html
id: 151
categories:
  - 'NULL'
date: 2007-11-09 10:00:00
---

在flash remoting服务器的根目录安置crossdomain.xml『这点很重要，我的amfphp在子目录下，于是我就吧crossdomain.xml放在子目录中但是没用。一定要放在根目录』

crossdomain.xml

  
  
   

以上的格式将允许所有来路访问

  
   
   
   
  amazon.com" secure="true" />  
  www.amazon.com" secure="true" />  
  pre-prod.amazon.com" secure="true" />  
  devo.amazon.com " secure="true" />  
  images.amazon.com" secure="true" />  
  anon.amazon.speedera.net" secure="true" />  
   
   
   
   
   
   
   
 

以上是 amazon的crossdomain 指定域名可以访问

flash player 会去读取该策略文件来决定这次跨域访问是否是合法的。只有在通过 HTTP、HTTPS 或 FTP 进行通讯的服务器上，策略文件才起作用。策略文件特定于所在服务器的端口和协议。

例如，策略文件位于 [https://www.thedomain.com:8080/crossdomain.xml](https://www.thedomain.com:8080/crossdomain.xml)，它只适用于在端口 8080 通过 HTTPS 对 [www.thedomain.com](http://www.thedomain.com) 进行的数据加载调用。

  
 

humen1 Tech