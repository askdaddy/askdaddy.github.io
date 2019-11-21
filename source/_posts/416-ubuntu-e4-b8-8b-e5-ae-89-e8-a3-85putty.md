---
title: Ubuntu 下安装PuTTY
tags:
  - linux
  - ssh
  - Ubuntu
  - unix
url: 416.html
id: 416
categories:
  - linux桌面
date: 2011-10-21 09:25:04
---

如题，ubuntu上我一直是直接用ssh的但是有一个缺点就是老要输入xxx@yyy putty可以记录，就爱这个。 以前在nokia E71 上也装了putty 好用，于是想在ubuntu上也装个，看了下官网，还真可以。 **Step 1.** 打开下面的下载页： http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html 找到 Unix source code 那一段 Release source code for Unix Source: putty-version.tar.gz (or by FTP) (RSA sig) (DSA sig) 把源码下下来，找个地方放，解压。 **Step 2.** #cd /path/to/putty-version/ #cd unix 注意了 要进入到里面的unix目录。 **Step 3.** #./configure #make -f Makefile.gtk #make install 又要注意在编译安装时如果不用.gtk的Mf那你就看不到图像界面了。 图像界面需要Gtk+ 2.0的支持 别忘了装 libgtk-dev **Last Step .** 跑起～ $putty /*******************************************************************/