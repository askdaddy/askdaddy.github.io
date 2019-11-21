---
title: OSX创建 Dock Stack
tags:
  - dock
  - osx
url: 881.html
id: 881
categories:
  - OS X
date: 2015-12-11 18:29:58
---

打开终端 \[code lang=bash\] defaults write com.apple.dock persistent-others -array-add '{ "tile-data" = { "list-type" = 1 ; }; "tile-type" = "recents-tile"; }' \[/code\] 然后 killall Dock