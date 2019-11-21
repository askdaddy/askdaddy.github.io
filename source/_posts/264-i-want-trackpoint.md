---
title: I want trackpoint!
url: 264.html
id: 264
categories:
  - linux桌面
date: 2009-10-11 21:51:02
tags:
---

本子是IBM R60e 系统是 9.04 红帽＋中键的组合一直不能用，使用时真的很不便，在网上看到了篇文章就想try一下，果然有效。 1.首先键盘设定选择为 IBM生产 型号 R60 2.功能实现依赖 sysfsutils文件安装： sudo apt-get install sysfsutils 3.sudo gedit /etc/hal/fdi/policy/mouse-wheel.fdi 写入代码：

 true
2
6 7
4 5
4 5
true 

4.保存 重启。 5.在[http://sourceforge.net/projects/tpctl/](http://sourceforge.net/projects/tpctl/) 可以下载一个 configure-trackpoint\_0.7-1\_i386.deb 功能完全可用