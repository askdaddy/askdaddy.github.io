---
title: install ibus on Ubuntu
tags:
  - Ubuntu
url: 291.html
id: 291
categories:
  - linux桌面
date: 2009-12-08 09:45:45
---

iBus 1.2 * intrepid: deb http://ppa.launchpad.net/ibus-dev/ibus-1.2-intrepid/ubuntu intrepid main * jaunty: deb http://ppa.launchpad.net/ibus-dev/ibus-1.2-jaunty/ubuntu jaunty main * karmic: deb http://ppa.launchpad.net/ibus-dev/ibus-1.2-karmic/ubuntu karmic main IBus 1.1 Main Page: https://launchpad.net/~ibus-dev/+archive/ppa 8.04: Hardy not supported. 8.10 Intrepid 1. add following line to /etc/apt/sources.list, deb http://ppa.launchpad.net/ibus-dev/ppa/ubuntu intrepid main 2. run $ sudo apt-get update, 3. run $ sudo apt-get install ibus ibus-pinyin 4. run $ im-switch -s ibus 5. logout and re-login 9.04 Jaunty similar with 8.10, but use following line: deb http://ppa.launchpad.net/ibus-dev/ppa/ubuntu jaunty main 9.10 Karmic similar with 8.10, but use following line: deb http://ppa.launchpad.net/lidaobing/ibus-910/ubuntu karmic main