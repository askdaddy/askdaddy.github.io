---
title: 'CDT在ubuntu9.04上调试不能[cannot find new threads:generic error]  Fixed'
tags:
  - CDT
  - linux
url: 411.html
id: 411
categories:
  - c++
  - linux桌面
date: 2011-06-28 15:10:24
---

点开 Debug Configurations Environment页签 点New... 弹出的 New Environment Variable对话框 里这样填 Name：LD_PRELOAD Value：/lib/libpthread.so.0 OK