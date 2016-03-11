---
layout: post
title: php 静态方法
date: 2012-08-19 14:02:00
category: blog
description: php 静态方法
---

在类里边, 静态成员方法里, 只能使用静态属性, 静态方法, 不能使用 $this->examplefun();或者 $this->value;  应该使用类成员访问关键字: parent, self, 或者类名来访问.

关键字的作用:

parent/self::常量名 
parent/self::$静态变量名
类名对于属性的访问同parent\ self是一样的. 


* 注意: 普通变量不能使用关键字访问.应该使用$this->变量名的形式访问.


*对于成员方法,除了私有方法\ 被保护方法不能被直接调用,需要借助公共方法调用外,静态方法\ 普通方法都可以使用 类名::方法名() ; parent/self::方法名(); 的形式访问.

例:

<?php


class fu {

    static $val1 = '我是静态变量';
    const val2 = '我是常量,我不需要实例化就可以访问!';
    var $val3='is test';

    function norfunc1() {

        echo 'this is normal function.<br />';

    }


    static function stafunc1() {

        echo 'this is stafunc function.<br />';



    }

    function test1() {

        self::norfunc1();
        self::stafunc1();


    }

}


class zi extends fu {


    function test2() {

        parent::norfunc1();              // 访问父类的普通方法.

        parent::stafunc1();           //访问父类的静态的方法.
    }

   static function test3() {

        parent::norfunc1();              // 访问父类的普通方法.

        parent::stafunc1();           //访问父类的静态的方法.

    }

}



fu::test1();
zi::test2();
zi::test3();

?>










<?php


class fu {


   static function test1() {

        echo '我是静态方法.<br />';
    }


    function test2() {
        echo '我是私有方法.<br />';
    }

    private function test3() {

        echo '你不会看见我!';
    }
}

fu::test1();
fu::test2();
fu::test3();      /* 报错  Fatal error: Call to private method fu::test3() from context '' in D:\AppServ\www\bao.php on line 25*/

?>










<?php

class  fu {

    function test1() {

        self::test3();

    }

    static function test2() {

        self::test3();
    }


    private function test3() {

        echo '我需要借助公共函数掉用我.<br />';

    }

}

class zi extends fu {

    function test4() {

       // parent::test3();    //这里报错, 因为test3 是父类的私有方法不可以直接调用.需要调用 调用了该私有方法的公共方法 test2();
        parent::test2();      // test1() 也可以
    }
}
fu::test1();
fu::test2();
zi::test4();
?>