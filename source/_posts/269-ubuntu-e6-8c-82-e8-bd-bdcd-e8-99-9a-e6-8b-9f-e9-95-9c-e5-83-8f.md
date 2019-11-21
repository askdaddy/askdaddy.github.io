---
title: ubuntu 挂载CD虚拟镜像
url: 269.html
id: 269
categories:
  - linux桌面
date: 2009-10-21 14:42:09
tags:
---

Cue/Bin 镜像 (.cue/.bin) 必须转换才能使用. 使用bchunk可以转换. o 安装bchunk: sudo apt-get install bchunk o 使用bchunk转换: bchunk myfile.bin myfile.cue myfile 转换后会得到一个 .iso 下面是挂载一个ISO文件的方法： sudo mkdir /media/cdimage ＃建立一个文件夹作为ISO挂载点 sudo mount -o loop myfile.iso /media/cdimage ＃挂载ISO文件，使用参数 -o loop 使用你想挂载的iso文件代替myfile.iso。 挂载一个镜像文件使之能被写入，使用下面的命令： sudo mkdir /media/cdimage sudo mount -o rw,loop myfile.iso /media/cdimage 卸载镜像文件： sudo umount /media/cdimage rmdir /media/cdimage