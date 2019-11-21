---
title: 使用 elasticsearch+logstash 存储获取实时日志【cdn realtime analytics】
tags:
  - bigdata
  - cdn
  - elasticsearch
  - es
  - log
  - logstash
  - nginx
  - syslog-ng
url: 802.html
id: 802
date: 2014-07-02 14:48:11
---

安装的我就不写了。 主要说下方案 nginx 实时吐日志给syslog-ng via pipe syslog-ng 向logstash 推送日志 via internet udp logstash 把日志塞进elasticsearch 并index 发送方： nginx.conf \[bash\] # ... log\_format real\_time '- $time\_iso8601 $host $request\_time $status $bytes\_sent'; server { listen 80; server\_name my\_test\_rt; access\_log /dev/realtime.pipe real\_time; location /{ proxy\_pass http://backend.com; } } # ... \[/bash\] syslog-ng.conf \[bash\] source s\_pipe { pipe("/dev/realtime.pipe"); }; destination d\_udp { udp("127.0.0.1" port(9999) template ("$MSG\\n") ); }; log {source(s\_pipe); destination(d\_udp); }; \[/bash\] \[bash\] #创建一个管道： makefifo /dev/realtime.pipe #先启动syslog-ng #不然nginx启动时会卡住 service syslog-ng start service nginx start \[/bash\] 接收方： /etc/logstash/conf.d/rt.conf \[bash\] input { udp { port =>9999 } } filter { grok { pattern => \["%{TIMESTAMP\_ISO8601:timestamp} %{IPORHOST:host} %{IPORHOST:domain} %{NUMBER:request\_time} %{NUMBER:status} %{NUMBER:bytes\_sent}" \] } mutate { remove\_field => \[ "message", "@version" \] } } output { elasticsearch { host => "127.0.0.1" flush\_size => 1 index => "rt-%{+YYYY.MM.dd.HH.mm}" } } \[/bash\] 把logstash 和 elasticsearch 都启动 。整个体系就运转起来了