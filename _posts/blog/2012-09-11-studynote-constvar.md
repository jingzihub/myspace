---
layout: post
title: php 中的常量
date: 2012-09-11 15:09:00
category: blog
description: php 中的常量
---

可以将常量名赋值给一个变量,用 constant函数输出常量的值.

例:

<?php

define('COUNT','value',true); 
$test = "count";
echo constant($test);

define('COUN',"$value",true);       // 将一个变量当做是常量的值, 往往不会输出. 

$value = 'is value .';               
echo constant("coun");

define('test','baby');
$arr = array(1,'baby'=>'is baby .','test'=>3);
echo $arr[test]              // 省略掉 单引号后, 系统将寻找常量test, 而不是去寻找 数组的键值 test . 
?>