---
title: 不能用outlook发信？(freebsd sendmail)
tags:
  - unix
url: 135.html
id: 135
categories:
  - 'NULL'
date: 2007-12-18 16:58:00
---

在女朋友家用adsl不能从公司的smtp发送邮件。为什么呢？问了老大才解决了这个低级问题。

原来ip没有被授权

  
解决方法：

添加ip到/etc/mail/access  
然后生成map文件

\# makemap hash /etc/mail/access.map < /ec/mail/access  
  
 

humen1 Tech