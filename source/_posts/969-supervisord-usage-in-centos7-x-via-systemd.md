---
title: 'supervisord usage in Centos7.x (via: systemd)'
tags:
  - python
  - supervisor
  - systemd
url: 969.html
id: 969
comments: false
categories:
  - linux server
date: 2016-04-05 15:18:23
---

1.  yum install python-setuptools python-pip
2.  pip install supervisor
3.  echo\_supervisord\_conf > /etc/supervisord.conf
4.  create init script in : /usr/lib/systemd/system/supervisord.service  
    ``` \[Unit\] Description=supervisord - Supervisor process control system for UNIX Documentation=http://supervisord.org After=network.target \[Service\] Type=forking ExecStart=/usr/bin/supervisord -c /etc/supervisord.conf ExecReload=/usr/bin/supervisorctl reload ExecStop=/usr/bin/supervisorctl shutdown User=root</li> </ol> \[Install\] WantedBy=multi-user.target <pre><code>```