---
layout: post
title: "php 正则表达式"
date: 2013-07-12 23:00:00
category: blog
description: "php 正则表达式"
---
这个模式与"&5"、"g7"及"-2"是匹配的，但与"12"、"66"是不匹配的。下面是几个排除特定字符的例子：

[^a-z] //除了小写字母以外的所有字符 
[^\\\/\^] //除了(\)(/)(^)之外的所有字符 
[^\"\'] //除了双引号(")和单引号(')之外的所有字符 
