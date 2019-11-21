---
title: >-
  TrafficServer源码：the possible operations or msg types sent from remote client
  to TM
tags:
  - ATS
  - cdn
  - trafficserver
url: 834.html
id: 834
categories:
  - ats
  - CDN
  - linux server
date: 2014-12-17 17:25:32
---

\[cpp\] // trafficserver/mgmt/api/NetworkMessage.h typedef enum { FILE\_READ, FILE\_WRITE, RECORD\_SET, RECORD\_GET, PROXY\_STATE\_GET, PROXY\_STATE\_SET, RECONFIGURE, RESTART, BOUNCE, EVENT\_RESOLVE, EVENT\_GET\_MLT, EVENT\_ACTIVE, EVENT\_REG\_CALLBACK, EVENT\_UNREG\_CALLBACK, EVENT\_NOTIFY, /* only msg sent from TM to client */ SNAPSHOT\_TAKE, SNAPSHOT\_RESTORE, SNAPSHOT\_REMOVE, SNAPSHOT\_GET\_MLT, DIAGS, STATS\_RESET\_NODE, STATS\_RESET\_CLUSTER, STORAGE\_DEVICE\_CMD\_OFFLINE, RECORD\_MATCH\_GET, API\_PING, SERVER\_BACKTRACE, UNDEFINED\_OP /* This must be last */ } OpType; \[/cpp\]