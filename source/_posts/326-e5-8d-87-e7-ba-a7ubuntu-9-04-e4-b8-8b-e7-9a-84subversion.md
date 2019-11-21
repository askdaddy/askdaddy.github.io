---
title: 升级ubuntu 9.04下的subversion
url: 326.html
id: 326
categories:
  - linux桌面
date: 2010-03-19 20:55:11
tags:
---

deb http://ppa.launchpad.net/anders-kaseorg/subversion-1.6/ubuntu jaunty main deb-src http://ppa.launchpad.net/anders-kaseorg/subversion-1.6/ubuntu jaunty main 增加源然后更新 然后： sudo apt-get update 删除当前版本的svn： sudo apt-get remove subversion 安装新版本的svn： sudo apt-get install subversion 查看新版本： svn –version svn，版本 1.6.5 (r38866) 编译于 Sep 2 2009，05:13:23