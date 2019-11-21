---
title: 'Fixed -> error: ‘umask’ was not declared in this scope '
tags:
  - linux
url: 370.html
id: 370
categories:
  - c++
  - linux桌面
date: 2010-12-20 12:43:16
---

在编译报错的那个cpp里加入

#include <sys/stat.h>

In linux