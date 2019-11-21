---
title: 'fms3启动时产生错误libnspr4.so [centos4.6]'
url: 86.html
id: 86
categories:
  - 'NULL'
date: 2008-03-26 20:18:00
tags:
---

./shmrd: error **while** loading shared libraries: libnspr4.so: cannot open shared object file: No such file or directory  
  
于是  
  
\# wget [http://download.opensuse.org/distribution/10.2/repo/oss/suse/i586/mozilla-nspr-4.6.3-10.i586.rpm](http://download.opensuse.org/distribution/10.2/repo/oss/suse/i586/mozilla-nspr-4.6.3-10.i586.rpm)  
\# cd /opt/adobe/fms/  
\# ls  
\# rpm -ivh mozilla-nspr-4.6.3-10.i586.rpm  
  
之后重启fms问题解决  
  
  

humen1 Tech