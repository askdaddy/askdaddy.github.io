---
title: ERROR 1418 (HY000) log_bin_trust_function_creators 解决
tags:
  - 数据库
url: 75.html
id: 75
categories:
  - 'NULL'
date: 2008-05-06 15:49:00
---

今天要写一个函数.但没有办法建提示错误如下:  
ERROR 1418 (HY000): This function has none of DETERMINISTIC, NO SQL, or READS SQL DATA in its declaration and binary logging is enabled (you \*might\* want to use the less safe log\_bin\_trust\_function\_creators variable)  
  
解决方式:(编缉my.cnf,添加如下)  
\[mysqld\]  
log\_bin\_trust\_routine\_creators = 1  
重启mysql就好了  

humen1 Tech