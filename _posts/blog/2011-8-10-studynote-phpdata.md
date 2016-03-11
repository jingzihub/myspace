---
layout: post
title: 关于php数据处理
date: 2011-08-10 15:40:00
category: blog
description: 关于php数据处理
---
num 为正数时,

ceil 往前进一位, 不管小数第一位是否大于5.

floor 一直保持原值.

round 预5进一.


num 为负数时,

ceil 一直保持原值.

floor 往后退一位.

round 预5进一.



<?php

$a = -10.1;

echo 'ceil'.ceil($a);

echo '<hr>';

echo 'floor'.floor($a);

echo '<hr>';

echo 'round'. round($a);

?>
