---
layout: post
title: "php 未赋值与已赋值的区别"
date: 2013-10-31 23:00:00
category: blog
description: "php 未赋值与已赋值的区别"
---

<?php
echo '未赋值:';
var_dump($a);
echo '<br />';

echo '赋值为空';
$a = '';
var_dump($a);
echo '<br />';

echo '赋值为空指针';
$a = null;
var_dump($a);
echo '<br />';

echo '销毁';
$a = 12;
unset($a);
var_dump($a);
?>