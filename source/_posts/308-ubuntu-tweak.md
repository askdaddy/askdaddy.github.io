---
title: Ubuntu Tweak
url: 308.html
id: 308
categories:
  - linux桌面
date: 2009-12-14 22:21:12
tags:
---

How to add the source of Ubuntu Tweak 添加源 open your terminal, first import the key: 开一控制台终端，下载及添加密钥 sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com FE85409EEAB40ECCB65740816AF0E1940624A220 type the command to run gedit(or other editor in your opinion) to modify the sources.list: 编辑/etc/apt/sources.list文件，按照你的Ubuntu版本加入下面两行： sudo gedit /etc/apt/sources.list And put the two line into it(If you are using Ubuntu 8.04 Hardy or early) : （注：我一般用System->Administration->Software Sources管理器添加第三方源） deb http://ppa.launchpad.net/tualatrix/ubuntu hardy main deb-src http://ppa.launchpad.net/tualatrix/ubuntu hardy main Or Ubuntu 8.10 Intrepid: deb http://ppa.launchpad.net/tualatrix/ubuntu intrepid main deb-src http://ppa.launchpad.net/tualatrix/ubuntu intrepid main Or Ubuntu 9.04 Jaunty: deb http://ppa.launchpad.net/tualatrix/ubuntu jaunty main deb-src http://ppa.launchpad.net/tualatrix/ubuntu jaunty main Then update the source and install or upgrade Ubuntu Tweak: 然后更新源并安装Ubuntu Tweak。今后如有更新，系统会提示。 sudo apt-get update sudo apt-get install ubuntu-tweak if you have installed, just type: sudo apt-get dist-upgrade