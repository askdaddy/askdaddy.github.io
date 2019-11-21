---
title: 'SSH,telnet终端中文显示乱码解决办法 (CentOS 5.0 ）'
url: 34.html
id: 34
categories:
  - 'NULL'
  - 技术杂文
date: 2008-12-16 09:57:00
tags:
---

vi /etc/sysconfig/i18n

将内容改为

LANG="zh_CN.GB18030"  
LANGUAGE="zh\_CN.GB18030:zh\_CN.GB2312:zh_CN"  
SUPPORTED="zh\_CN.GB18030:zh\_CN:zh:en\_US.UTF-8:en\_US:en"  
SYSFONT="lat0-sun16"

humen1 Tech