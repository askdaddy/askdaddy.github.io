---
title: 'Flash Tracer -- For Lin :)'
tags:
  - flash
  - linux
url: 352.html
id: 352
categories:
  - linux桌面
  - 技术杂文
date: 2010-12-03 08:40:45
---

一直在用FF的一个插件叫flashtracer。觉得太麻烦，每次要用都要先开FF。 其实原理很简单不就是度flash echo出来的文本log么，直接在Terminal里显示出来不就好了

#/bin/bash
echo "\\033\]0; \[Flash Tracer\] \\007"
tail -f ~/.macromedia/Flash_Player/Logs/flashlog.txt 

哦，我是在linux里开发AS的～