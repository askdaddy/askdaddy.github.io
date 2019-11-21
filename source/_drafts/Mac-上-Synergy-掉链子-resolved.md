---
title: 'Mac 上 Synergy 掉链子[resolved]'
tags:
  - mac
  - posts
  - synergy
url: 1089.html
id: 1089
comments: false
categories:
  - Evernote
---

用mac的人经常不关机，只是合上盖子，我发现Synergy在2.x以后将功能和UI分离了。UI的问题是太简略了，除了向官方推log没功能。 提供功能的Service 经常掉链子，还不能用UI搞定，于是运行以下命令强杀之

ps aux|grep synergy|grep service|awk '{print $2}' |xargs kill -9

杀掉后Synergy会自己起Service。