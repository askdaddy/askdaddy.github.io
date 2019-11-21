---
title: php-fpm 的启动，关闭 ，重启脚本【shell】
tags:
  - php
url: 408.html
id: 408
categories:
  - linux桌面
date: 2011-06-04 21:32:46
---

新建一个shell脚本然后输入。 \[bash\] #!/bin/sh # # php-fpm - this script starts and stops the daemin # Source function library. . /etc/rc.d/init.d/functions # Source networking configuration. . /etc/sysconfig/network # Check that networking is up. \[ "$NETWORKING" = "no" \] && exit 0 php="/usr/local/sbin/php-fpm" prog=$(basename $php) CONF\_FILE="/usr/local/lib/php.ini" lockfile=/var/lock/subsys/php-fpm start() { \[ -x $php \] || exit 5 \[ -f $CONF\_FILE \] || exit 6 echo -n $"Starting $prog: " daemon $php -c $CONF\_FILE retval=$? echo \[ $retval -eq 0 \] && touch $lockfile return $retval } stop() { echo -n $"Stopping $prog: " killproc $prog -QUIT retval=$? echo \[ $retval -eq 0 \] && rm -f $lockfile return $retval } restart() { configtest || return $? stop start } reload() { configtest || return $? echo -n $"Reloading $prog: " killproc $php -HUP RETVAL=$? echo } force\_reload() { restart } configtest() { $php -t -c $CONF\_FILE } rh\_status() { status $prog } rh\_status\_q() { rh\_status >/dev/null 2>&1 } case "$1" in start) rh\_status\_q && exit 0 $1 ;; stop) rh\_status\_q || exit 0 $1 ;; restart|configtest) $1 ;; reload) rh\_status\_q || exit 7 $1 ;; force-reload) force\_reload ;; status) rh\_status ;; condrestart|try-restart) rh\_status_q || exit 0 ;; *) echo $"Usage: $0 {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}" exit 2 esac \[/bash\]