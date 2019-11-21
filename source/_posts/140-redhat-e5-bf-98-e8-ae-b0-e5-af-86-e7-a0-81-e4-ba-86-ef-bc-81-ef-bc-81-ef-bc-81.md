---
title: redhat忘记密码了！！！
tags:
  - linux
url: 140.html
id: 140
categories:
  - 'NULL'
date: 2007-12-21 17:51:00
---

默认的引导装载程序 GRUB ！  
在引导装载程序菜单上，键入 \[e\] 来进入编辑模式。  
  
　　你会面对一个引导项目列表。查找其中类似以下输出的那一行：  
  
　　 kernel /vmlinuz-2.4.18-0.4 ro root=/dev/hda2  
  
　　按箭头键直到这一行被突出显示，然后按 \[e\] 。  
  
　　按一下空格键来添加一个空格，然后添加 single 来通知 GRUB 引导单用户 Linux 模式。按 \[Enter\] 键来使编辑结果生效。  
  
　　你会被带回编辑模式屏幕，从这里，按 \[b\] ，GRUB 就会引导单用户 Linux 模式。载入结束后，你会面对一个类似以下的 shell 提示：  
  
　　 sh-2.05#  
  
　　现在，你便可以改变root命令，键入：  
  
　　 sh-2.05# passwd root  
  
　　你会被要求重新键入口令来校验。结束后，口令就会被改变，你便可以在提示下键入 reboot 来重新引导；然后，象平常一样登录为根用户。

humen1 Tech