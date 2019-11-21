---
title: Install MongoDB on Windows — MongoDB Manual 3.2
tags:
  - mongo
url: 907.html
id: 907
comments: false
categories:
  - Windows
date: 2016-01-08 17:18:20
---

> MongoDB Manual 3.2 Install MongoDB on Windows

来源： _[Install MongoDB on Windows — MongoDB Manual 3.2](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-windows)_     添加windows service 成功 \[bash\] sc.exe create MongoDB binPath="C:\\Program Files\\MongoDB\\Server\\3.2\\bin\\mongod.exe" --service --config="C:\\Program Files\\MongoDB\\mongo.cfg" DisplayName= "MongoDB" start= "auto" \[/bash\]