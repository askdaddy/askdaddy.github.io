---
title: letsencrypt.org  1st. step
url: 937.html
id: 937
categories:
  - security
date: 2016-01-20 22:12:55
tags:
---

https://letsencrypt.org/ [![屏幕快照 2016-01-20 14.37.41](/uploads/2016/01/屏幕快照-2016-01-20-14.37.41.png)](/uploads/2016/01/屏幕快照-2016-01-20-14.37.41.png) 这是一个由很多个互联网巨头攒起来的非营利性组织。 来瞥一眼有哪些巨头： [![屏幕快照 2016-01-20 14.39.39](/uploads/2016/01/屏幕快照-2016-01-20-14.39.39.png)](/uploads/2016/01/屏幕快照-2016-01-20-14.39.39.png)   好了，简单来说就一句话：提供免费的秒生web 证书！！！！！！！！！（此处省略n个！）   我就拿来测试了。 假设我们要给 ssl.humen1.net 生成证书 。生成证书的server ip 为 11.11.11.11

*   先将 ssl.humen1.net A 11.11.11.11
*   在server上配置nginx

\[bash\] server { listen 80; listen 443 ssl; server\_name ssl.humen1.net; ssl\_certificate /etc/letsencrypt/live/ssl.humen1.net/fullchain.pem; ssl\_certificate\_key /etc/letsencrypt/live/ssl.humen1.net/privkey.pem; location / { root /data/letsencrypt; index index.html; } } \[/bash\]

*   安装letsencrypt

\[bash\] $ git clone https://github.com/letsencrypt/letsencrypt $ cd letsencrypt $ ./letsencrypt-auto --help \[/bash\]

*   ./letsencrypt-auto certonly --webroot -w /data/letsencrypt -d ssl.humen1.net