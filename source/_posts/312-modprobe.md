---
title: modprobe
url: 312.html
id: 312
categories:
  - linux server
date: 2009-12-25 22:48:47
tags:
---

modprobe(module probe) 功能说明：自动处理可载入模块。 语　　法：modprobe \[-acdlrtvV\]\[--help\]\[模块文件\]\[符号名称 = 符号值\] 补充说明：modprobe可载入指定的个别模块，或是载入一组相依的模块。modprobe会根据depmod所产生的相依关系，决定要载入哪些模块。若在载入过程中发生错误，在modprobe会卸载整组的模块。 参　　数： -a或--all 　载入全部的模块。 -c或--show-conf 　显示所有模块的设置信息。 -d或--debug 　使用排错模式。 -l或--list 　显示可用的模块。 -r或--remove 　模块闲置不用时，即自动卸载模块。 -t或--type 　指定模块类型。 -v或--verbose 　执行时显示详细的信息。 -V或--version 　显示版本信息。 -help 　显示帮助。