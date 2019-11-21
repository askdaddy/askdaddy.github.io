---
title: >-
  启动apache出现(2)No such file or directory: Failed to enable the 'httpready'
  Accept Filter
url: 84.html
id: 84
categories:
  - 'NULL'
date: 2008-04-01 01:39:00
tags:
---

Freebsd启动apache出现  
\[warn\] (2)No such file or directory: Failed to enable the 'httpready' Accept Filter  
  
找到/boot/loader.conf并修改，输入：  
  
accf\_http\_load="yes"  
  
然后保存就可以了！  
  

humen1 Tech