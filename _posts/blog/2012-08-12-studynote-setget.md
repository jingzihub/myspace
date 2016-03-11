---
layout: post
title: php set和get用法
date: 2012-08-12 11:03:00
category: blog
description: php set和get用法
---

<?php

class test {

    private $name;
    private $age;

    function __set($proname,$value) {
        echo "{$this->$proname}调用__set方法.<br />";
        $this->$proname=$value;
    }

    function __get($proname) {
       return "{$this->$proname}调用__get方法.<br />";
    }


}

$test = new test;
echo $test->name='林林';
echo '<br />';
echo $test->name;
echo '<br />';

echo $test->age='100';
echo '<br />';
echo $test->age;
echo '<br />';


echo $test->sex='female';
echo '<br />';

echo $test->sex;
echo '<br />';
echo '<br />';

echo $test->age='1000';
echo '<br />';
echo '<br />';
echo $test->my='test';
echo '<br />';
echo $test->my;

?>


已定义未赋值的私有变量在赋值时调用 __set方法.再对变量尽享赋值.

在对未定义的变量查询时, 会先调用__get方法确认该变量不存在.然后调用__set()方法, 为变量赋值,默认该变量为public.

执行顺序:
echo $test->age='1000';                   // age 已定义,私有 

    __set()   ->     echo 
   设age的值         输出运算后的值

--------------------------------------------------------

echo $test->age='1000';                 // age 已定义,公共 

    echo 
    输出运算后的值

---------------------------------------------------------

echo $test->age='1000';                   // age未定义 

__get()   - >    __set()   ->     echo 
取age的值        设age的值         输出运算后的值

----------------------------------------------------------






__get()
读取一个对象的属性时，
若属性存在，则直接返回属性值；
若不存在，则会调用__get函数。

__set()
设置一个对象的属性时，
若属性存在，则直接赋值；
若不存在，则会调用__set函数。
