---
layout: post
title: html学习记录
date: 2011-07-01 11:07:00
category: blog
description: html学习记录
---

*获取单选按钮的值

1. 设置value, 再直接通过get 或者post 获得.



*获取复选框的值

1. 例如, 有一个名为 book[] (必须存为数组)的 复选框, book[] 默认为一个空的数组. 用户选中的value 值将会存入 book[] 这个数组.

2. 获取book[] 的值, 即获取book数组的每一个元素, 用循环或者直接用 print_r 打印. 



*获取下拉框的值

1.直接获得.



*获取菜单列表的值

1. 设置name 为一个数组. 比如: test[] .用post 或者 get 获得后, 用循环或者 直接用 print_r 打印.



* form 表单 的 enctype = "multipart/form-data" 属性. 

为true时, $_files[upfile] 生效. 为false时, $_post[upfile]生效.
