---
title: PHP用array_push() array_reverse() array_pop()来模拟队列～
url: 44.html
id: 44
categories:
  - 'NULL'
date: 2008-10-28 14:01:00
tags:
---

$a = array(0=>1,1=>2,2=>3);//原始数组

print_r($a);

echo "

* * *

";  

  

$b = 4;//要入队的数

array_push($a,$b);//将$b压入数组的末尾（入栈）

print_r($a);

echo "

* * *

";  

  

$c = array_reverse($a);//将数组单元顺序颠倒

print_r($c);

echo "

* * *

";  

  

array_pop($c);//将颠倒后的数组最后一个单元弹出（出栈）

print_r($c);

echo "

* * *

";  

  

$d = array_reverse($c);//将数组顺序恢复

print_r($d);

echo "

* * *

";  

?>

humen1 Tech