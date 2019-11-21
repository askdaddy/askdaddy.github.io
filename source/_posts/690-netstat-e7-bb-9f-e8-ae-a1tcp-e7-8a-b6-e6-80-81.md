---
title: netstat统计tcp状态
tags:
  - network
url: 690.html
id: 690
categories:
  - linux server
date: 2014-01-06 11:49:58
---

\[bash\]netstat -ant | awk '/^tcp/{++State\[$NF\]} END {for (key in State) print key,State\[key\]}'\[/bash\]