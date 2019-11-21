---
title: 解决‘preg_match() repeated subpattern is too long’ 的问题
url: 33.html
id: 33
categories:
  - 'NULL'
  - 技术杂文
date: 2008-12-17 09:16:00
tags:
---

还记得之前写了篇文章[http://www.humen1.net/2008/10/dz.html](http://www.humen1.net/2008/10/dz.html)  
这篇文章写了我引用dz论坛的文字过滤机制。  
最近因为迁移程序到不同的服务器环境下出现了'preg_match() repeated subpattern is too long' 的问题。原因如下

在php bug 里有这篇文章[http://bugs.php.net/bug.php?id=39415&edit;=3](http://bugs.php.net/bug.php?id=39415&edit=3)  
最后由高人指点说是PCRE的版本问题。对比了我两台服务器的PCRE版本，的确新服的版本是6.6而老服的版本是6.7那我就暂定是这个原因导致的。不过新服用的是centos5.2做为OS，使用yum更新PCRE说6.6是最高版本了。大家都知道centos  
使用不是"非常新"（bleeding-edge,指一种最新的，因而也并非完美的技术。使用者为了尝鲜，就要付出稳定性和效率的代价。）的软件导致我更新不到6.7  
那怎么办呢？  
想想人家错误写的很明白subpattern is too long 正则表达式太长了么，那我就分段来咯。  
下面这段是老程序  
function censorChk($message){  
$flag = 0;  
$censor = array();//这里的array是所有屏蔽字数组。

$banned = '/('.implode('|', $cell).')/i';  
if (preg\_match($banned, preg\_replace('/\\s*|\\\[\[^\\\]\]*\\\]/i',  
'', $message))){  
$flag = 1;  
}

return $flag;  
}

修改后成为  
function censorChk($message){  
$flag = 0;  
$censor = array();//这里的array是所有屏蔽字数组。  
$allChunk = array_chunk($censor,500);//把原始数组分割为n块，每块的长度500  
foreach ($allChunk as $cell){  
$banned = '/('.implode('|', $cell).')/i';  
if (preg\_match($banned, preg\_replace('/\\s*|\\\[\[^\\\]\]*\\\]/i',  
'', $message))){  
$flag = 1;  
}  
}

return $flag;  
}

这样从程序上解决PCRE的限制

humen1 Tech