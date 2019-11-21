---
title: apache 只允许某个ip访问某个目录
url: 79.html
id: 79
categories:
  - 'NULL'
date: 2008-04-08 11:12:00
tags:
---

在  之间+上  
  
  
            Order allow,deny  
            Allow from [220.234.206.194](http://220.234.206.194)  
            Allow from [127.0.0.1](http://127.0.0.1)  
   
  
/dir  就是你要禁止其他主机访问的目录  
Order allow,deny 启用 allow和deny指令  
allow xxx 允许xxx通过其他屏蔽  
deny xxx 屏蔽xxx其他通过  
  
我要的效果是只有我的本机ip能访问此目录所以我+上了我的ip220.234.206.194  
保险起见吧本机的ip127.0.0.1也+上不然cgi程序跑起来可能有问题。  
  

humen1 Tech