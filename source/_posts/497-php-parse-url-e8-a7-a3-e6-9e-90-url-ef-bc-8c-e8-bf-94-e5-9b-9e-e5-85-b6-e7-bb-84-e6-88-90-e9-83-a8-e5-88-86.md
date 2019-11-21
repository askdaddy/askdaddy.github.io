---
title: 'PHP: parse_url  解析 URL，返回其组成部分'
tags:
  - 解析url
url: 497.html
id: 497
categories:
  - PHP专题
date: 2012-12-11 11:58:39
---

[PHP: parse_url - Manual](http://cn2.php.net/manual/zh/function.parse-url.php).

[mixed](http://cn2.php.net/manual/zh/language.pseudo-types.php#language.types.mixed) **parse_url** ( string `$url` \[, int `$component` = -1 \] )

本函数解析一个 URL 并返回一个关联数组，包含在 URL 中出现的各种组成部分。

本函数_不是_用来验证给定 URL 的合法性的，只是将其分解为下面列出的部分。不完整的 URL 也被接受， **parse_url()** 会尝试尽量正确地将其解析。

2个参数

_`url`_

要解析的 URL。无效字符将使用 ___ 来替换。

_`component`_

指定

**`PHP_URL_SCHEME`**、 **`PHP_URL_HOST`**、 **`PHP_URL_PORT`**、

 **`PHP_URL_USER`**、**`PHP_URL_PASS`**、 **`PHP_URL_PATH`**、

**`PHP_URL_QUERY`** 或 **`PHP_URL_FRAGMENT`**

的其中一个来获取 URL 中指定的部分的 [string](http://cn2.php.net/manual/zh/language.types.string.php)。 （除了指定为 **`PHP_URL_PORT`** 后，将返回一个[integer](http://cn2.php.net/manual/zh/language.types.integer.php) 的值）。

  返回值

对严重不合格的 URL， **parse_url()** 可能会返回 **`FALSE`**。

如果省略了 _`component`_ 参数，将返回一个关联数组 [array](http://cn2.php.net/manual/zh/language.types.array.php)，在目前至少会有一个元素在该数组中。数组中可能的键有以下几种：

*   scheme \- 如 http
*   host
*   port
*   user
*   pass
*   path
*   query \- 在问号 _?_ 之后
*   fragment \- 在散列符号 _#_ 之后

如果指定了 _`component`_ 参数， **parse_url()** 返回一个 [string](http://cn2.php.net/manual/zh/language.types.string.php) （或在指定为 **`PHP_URL_PORT`** 时返回一个[integer](http://cn2.php.net/manual/zh/language.types.integer.php)）而不是 [array](http://cn2.php.net/manual/zh/language.types.array.php)。如果 URL 中指定的组成部分不存在，将会返回 **`NULL`**。