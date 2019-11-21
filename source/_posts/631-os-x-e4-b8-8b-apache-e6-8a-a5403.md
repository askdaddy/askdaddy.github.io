---
title: OS X 下 apache 报403
tags:
  - apache
  - osx
url: 631.html
id: 631
categories:
  - OS X
date: 2013-07-15 23:21:34
---

错误如下： You don't have permission to access /   ... 我启用了 http-vhosts.conf DocumentRoot 设在了我的home目录里具体目录为  /User/seven/www， 属主是seven这个用户 我发现os x apache 的用户是 _www 但是系统里没有这个用户的信息，一番research后找到了解决方案。 到/etc/apache2/users 下创建文件 Seven.conf \[text\] <Directory "/Users/seven/www/"> Options Indexes MultiViews AllowOverride All Order allow,deny Allow from all </Directory> \[/text\]   重启apache就OK了 \[bash\] apachectl restart \[/bash\]