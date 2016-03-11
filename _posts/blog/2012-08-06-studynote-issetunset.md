---
layout: post
title: php isset和unset用法
date: 2011-08-06 17:33:00
category: blog
description: php isset和unset用法
---

isset 

访问不存在的变量,函数都会有两次输出.

例:

<?php

class Testt {
  //  var $a;  //这样就不输出
  //  public $a;  //这样也不输出

    protected $a;  //输出 你小子偷看我??
  //  private $a;  //输出 你小子偷看我??

    public function __construct($value) {
        $this->a = $value;
    }

    public function __isset($name) {
        echo "你小子偷看我??";
        return isset($this->a);  //返回真是的信息
    }

    public function __unset($name) {
        echo "你没权利宰了我!";
        unset($this->$name);
    }

    function istest($proname) {

        echo "您要查看的是:{$this->$proname}";
    }
}
$test = new Testt("我是a");
isset($test->a);
unset($test->a);
var_dump($test->istest(a));
isset($test->a);
isset($test->b);

?>




unset 




<?php

class Testt {

    var $name = 'baby';
    protected $a = 'is a';




    public function __unset($name) {
        echo "你没权利宰了我!";
        unset($this->$name);
        return ;
    }
    function fun($proname) {

        echo "结果是{$this->$proname}.";
    }

    function __get($proname) {

        echo "结果是{$this->$proname}.";
    }

}

$obj = new testt;
echo 'get访问私有属性:';
$obj->a;
echo '<br>';
echo '用自定义函数访问私有属性:';
$obj->fun(a);
echo "<hr />";
echo 'unset卸载私有属性.';
unset($obj->a);
echo "<hr />";
echo 'get访问私有属性.';
$obj->a;
echo '<br />';
echo '自定义函数访问私有属性.';
$obj->fun(a);
echo "<hr />";

echo '直接输出公有属性. ';
echo $obj->name.'<br>';
echo 'unset卸载公有属性 .';
unset($obj->name);
echo '<br />';
echo 'get访问此公有属性 .';
$obj->name;
echo '<br />';
echo '自定义函数访问此公有属性 .';
$obj->fun(name);
echo '<br />';

echo "<hr />";

echo 'get访问未定义属性:';
$obj->age;
echo '<br />';
echo '用自定义函数访问未定义属性:';
$obj->fun(age);
echo '<br />';

?>



总结得出:

__get()方法, 有值输出, 没有就不输出.