---
title: apache压力测试
tags:
  - php
url: 92.html
id: 92
categories:
  - 'NULL'
date: 2007-12-27 11:02:00
---

测试脚本index.php内容为：  
phpinfo();  
?>;  
  
用10000个连接，200个并发连接测试：  
  
ab -n 10000 -c 200 [http://localhost/index.php](http://localhost/index.php)  

humen1 Tech