---
title: 'sendmail.群发[freebsd]'
tags:
  - unix
url: 99.html
id: 99
categories:
  - 'NULL'
date: 2007-12-24 23:16:00
---

  
今天弄清了怎么实现群发功能，设置一个 [all@domain.com](mailto:all@domain.com)的邮箱地址当向这个地址发送邮件时可以发送给指定用户

在sendmail的设置文件里有这样一支/etc/mail/aliases

我们vi它

最后+上

all: [xxx@domain.com,xxx1@domain.com](mailto:xxx@domain.com,xxx1@domain.com)

保存

#makemap hash /etc/mail/aliases.db < /etc/mail/aliases  
 

好了！！

humen1 Tech