---
title: c++ explode()
url: 276.html
id: 276
categories:
  - 技术杂文
date: 2009-11-09 14:52:33
tags:
---

用惯了php里的explode函数，迁移到c＋＋觉得无所适从 网上找了这个方法，经过验证可以使用，中文也行

/\*
 \* C++ Explode Function
 \* Written by Alec Hussey
 \* License: Public Domain
 */

#include #include #include #include std::vector explode(char *sep, std::string src)
{
	std::vector output;
	boost::char_separator separator(sep);
	boost::tokenizer \> tokens(src, separator);
	boost::tokenizer >::iterator token_iter;

	for (token\_iter = tokens.begin(); token\_iter != tokens.end(); token_iter++)
		output.push\_back(*token\_iter);

	return output;
}