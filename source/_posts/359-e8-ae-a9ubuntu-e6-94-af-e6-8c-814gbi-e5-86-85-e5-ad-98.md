---
title: 让ubuntu 支持4Gbi内存
tags:
  - Ubuntu
url: 359.html
id: 359
categories:
  - linux桌面
  - 技术杂文
date: 2010-12-13 10:12:46
---

公司的台机给我加了2g内存，开机发现只认出3g（bios里是4g--硬件没问题） google一下有2个解决方案 1.装64位系统 2.换内核，换成server版内核，号称支持最多64g【前提是硬件要支持】 权衡一下我还是选方案2 具体操作我用的新立得直接装的-ubuntu的好处么

sudo apt-get install linux-restricted-modules-server  linux-image-server  linux-headers-server linux-server

装好重启就ok了。。。