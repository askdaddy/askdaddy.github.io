---
title: vm安装magic linux 分辨率问题
tags:
  - linux
url: 142.html
id: 142
categories:
  - 'NULL'
date: 2007-11-22 23:00:00
---

vm版本 5.5.3  
安装时候选了个默认显示器，分辨率选了800x600  
进了系统发现图形化显示器设置里的最大分辨率就是800x600  
网上搜索了一下原来是xorg.conf 这个文件里有配置  
  
具体位置可以用搜索来找  
打开文件  
首先是对显示器行频（水平分辨率）和场频（垂直分辨率）的设置在xorg.conf中有类似一段：Section "Monitor"  
Identifier "Monitor0"  
VendorName "Monitor Vendor"  
ModelName "206STUDIO"  
HorizSync 30.0 - 70.0  
VertRefresh 50.0 - 160.0  
EndSection  
  
其中HorizSync，VertRefresh分别是显示器行频（水平分辨率）和场频（垂直分辨率）的设置应该根据显示器的性能进行设置，他们的值决定了显示分辨率和刷新频率可能取值的范围。关于场频，行频，分辨率，刷新频率的具体含意及关系请大家补充。接着是对首先和可选分辨率的设置在xorg.conf中有类似一段：  
  
Section "Screen"  
Identifier "Screen0"  
Device "Videocard0"  
Monitor "Monitor0"  
DefaultDepth 24  
SubSection "Display"  
Depth 24  
Modes "1024x768" "800x600" "640x480"  
EndSubSection  
EndSection  
  
行 ： Modes "1024x768" "800x600" "640x480" 设置了三种可选的分辨率，排在最前面的就是首选的分辨率，也就是一般生效的分辨率。X启动时如果首选的分辨率无效，比如过高，会依次尝试后面的分辨率。这个例子中，最高的分辨率，排在最后，并不是首选的。  
  
重启就可以享受1024x768了

humen1 Tech