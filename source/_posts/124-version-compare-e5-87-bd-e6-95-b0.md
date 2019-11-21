---
title: version_compare ()函数
tags:
  - php
url: 124.html
id: 124
categories:
  - 'NULL'
date: 2007-11-30 11:36:00
---

**version_compare** ( string version1, string version2 \[, string operator\])  
 

对比php版本

str1 与str2  按照 string operator 规则（默认是 '>'）对比

真返回1 否返回-1 

// prints -1  
echo version_compare ("4.0.4", "4.0.6");  
  
// these all print 1  
echo version_compare("4.0.4" , "4.0.6", "<");  
echo version_compare("4.0.6", "4.0.6", "eq");  
?>

humen1 Tech