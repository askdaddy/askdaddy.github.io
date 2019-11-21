---
title: '将类路径转换为.语法路径传递给AS[PHP]'
tags:
  - php
url: 120.html
id: 120
categories:
  - 'NULL'
date: 2008-03-08 15:29:00
---

define("ROOT_PATH","/xxx/yyy/zzz/"); 

function A (){  
   $this->rootPath = ROOT_PATH;  
  $this->file = \_\_FILE\_\_;  
  return $this->classRoot = basename(str\_replace("/",".",str\_replace("$this->rootPath" ,"", $this->file)),".php");    
 }

humen1 Tech