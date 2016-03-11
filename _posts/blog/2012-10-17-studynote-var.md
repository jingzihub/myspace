---
layout: post
title: php中对值的判断
date: 2012-10-17 15:22:00
category: blog
description: php中对值的判断
---

//不要把字符这样来判断... 字符判断全部用 ===

var_dump('sfsdf' == 0);  //这叫数字对比了.  所有第一位非0的,全部是 0

false == 0;
null == 0;
false == null.