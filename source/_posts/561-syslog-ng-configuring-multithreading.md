---
title: syslog-ng Configuring multithreading
tags:
  - syslog-ng
url: 561.html
id: 561
categories:
  - linux server
date: 2013-04-01 15:18:17
---

To enable multithreading globally, use the threaded option: \[text\] options {threaded(yes) ; }; \[/text\] To enable multithreading only for a selected source or destination, use the flags("threaded") option: \[text\] source s\_tcp\_syslog { tcp(ip(127.0.0.1) port(1999) flags("syslog-protocol", "threaded") ); }; \[/text\]