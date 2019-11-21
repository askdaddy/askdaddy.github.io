---
title: linux ssd 格式化命令
tags:
  - ssd
url: 490.html
id: 490
categories:
  - linux server
date: 2012-12-06 18:27:33
---

新+了个ssd  设备 /dev/sdb1 （分区已经分好）以下是格式化命令 mkfs.ext4 -K -E stride=128,stripe-width=128 -O ^has_journal /dev/sdb1