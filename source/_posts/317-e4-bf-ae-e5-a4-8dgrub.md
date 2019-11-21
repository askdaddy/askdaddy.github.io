---
title: 修复grub
url: 317.html
id: 317
categories:
  - linux桌面
date: 2010-01-16 16:43:43
tags:
---

重装win7后，mbr被win7写入信息导致grub无法工作解决方法 从CD-ROM启动,从Live CD启动进入桌面。 打开终端或者切换到一个tty（Ctrl+Alt+F1）。 输入:sudo grub 输入:find /boot/grub/stage1 ##有人说这一步不用,不过个人感觉还是应该加上这一步 输入:root (hd0,x) ##输入find命令反馈的数据 输入:setup (hd0) ##如果想用xp进行多系统引导就写(hd0,x) 输入:quit ##退出grub。