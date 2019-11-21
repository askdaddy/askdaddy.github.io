---
title: hp dv4 ubuntu 9.04声音问题正解 （包含其他机型）
url: 314.html
id: 314
categories:
  - linux桌面
date: 2009-12-25 22:50:01
tags:
---

http://ubuntuforums.org/showthread.php?t=1043568 国外的ubuntu论坛上找来的，崇拜老外的分享精神，我用了3小时才找到正解。希望同样有 问题的人能节约这三小时 英文不怎么样的兄台我给点线索 主要要修改/etc/modprobe.d/alsa-base.conf文件 在文件尾加上一句 options snd-hda-intel xxx=xxx 两个xxx是重点部分，贴子里有各种机型对应的内容，都是老外收集的（感动！） 当然也有 alsa的重启方法，可以节约时间不用reboot（太周到了，我都感动的要流泪了） 支持开源OS