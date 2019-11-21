---
title: 在shell 脚本里嵌入python
tags:
  - python
  - shell
url: 831.html
id: 831
categories:
  - linux server
  - Python
date: 2014-12-08 14:57:07
---

\[shell\] #!/bin/bash function pytest() { python - $@ <<EOT import sys,datetime print 'Current Time is %s' % datetime.datetime.now() print sys.argv EOT } RT=$(pytest $@) echo my python script says: $RT \[/shell\]