---
title: Python timelib
tags:
  - python
url: 770.html
id: 770
categories:
  - Python
date: 2014-03-19 17:15:11
---

可以通过pip安装这个库   我是为了要使用和php中的 strtotime函数才用到的，很实用 获取上周的时间戳 \[python\] from timelib import strtotime from datetime import date if \_\_name\_\_=='\_\_main\_\_': print date.fromtimestamp(strtotime('-2 week Monday')) \[/python\]