---
title: php测试代码
url: 27.html
id: 27
categories:
  - 'NULL'
  - 技术杂文
date: 2008-12-17 17:32:00
tags:
---

在sitepoint上上看到一篇文章Good and Bad  
Code，是关于如何提高php代码的安全性、兼容性和性能的。其中有一段是介绍如何改进以下的这行php代码。这段代码经常被sitepoint用来测试php程序员应聘者。

<?  
echo("<p>Search results for query: " .$_GET\['query'\] . ".</p>");  
?>  
这段代码很适合用来测试一个php开发人员是否合格。因为这段代码并没有要求太多记忆上的东西，但是对代码的安全，性能，兼容性方面都做了考察。思考一下吧：-）

answers from sitepoint:

<?php  
if (isset($_GET\['query'\]))  
{  
echo '<p>Search results for query: ',  
htmlspecialchars($\_GET\['query'\], ENT\_QUOTES), '.</p>';  
}  
?>  
说明 ：

The "short" opening PHP tag (<?) has been replaced with the more  
portable (and XML-friendly) <?php form.  
Before attempting to output the value of $_GET\['query'\], isset is used  
to verify that it actually has a value.  
The unnecessary brackets (()) around the value passed to echo have been removed.  
Strings are delimited by single quotes instead of double quotes to  
avoid the performance hit of PHP searching for variables to  
interpolate within the strings.  
Rather than using the string concatenation operator (.) to pass a  
single string to the echo statement, the strings to be output by echo  
are separated by commas for a tiny performance boost.  
Passing the ENT_QUOTES argument to htmlspecialchars to ensure that  
single quotes (') are also escaped isn't strictly necessary in this  
case, but it's a good habit to get into.

humen1 Tech![](https://blogger.googleusercontent.com/tracker/7269874978253342363-6435391974436084045?l=www.humen1.net)