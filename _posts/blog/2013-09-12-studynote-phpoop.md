---
layout: post
title: "php 面向对象知识"
date: 2013-09-12 23:00:00
category: blog
description: "php 面向对象知识"
---
// private 、protected的属性和方法都不能在外部直接访问。必须通过 public成员方法调用(private属性或方法,protected属性或方法).public 属性或方法可以在外部直接访问。							
					
// $this ->属性 ; $对象名->属性/方法()；类名/parent/self::$属性/方法();		

//public private protected 变量均可在子类中重定义，  未定义则不输出。

//在类中定义一个变量, 该变量将会自动被设为public, 并且弹出一个警告.

//构造函数必须是public的.函数默认为是public的.


//变量输出需要先实例化对象,再调用,常量不需要实例化.常量的输出格式为  echo 类名::常量名 ; 

//静态变量  echo 类名::$静态变量名 ;



对象中的对象??
<?php
class A
{
   protected $prot;
   private $priv;
   
   public function __construct($a, $b)
   {
       $this->prot = $a;
       $this->priv = $b;
   }
   
   public function print_other(A $other)
   {
       echo $other->prot;
       echo $other->priv;
   }
}

class B extends A
{
}

$a = new A("组件", "组件");
$other_a = new A("other_a_protected", "other_a_private");

$b = new B("b_protected", "ba_private");

$other_a->print_other($a); //echoes a_protected and a_private
echo '<br />';
$other_a->print_other($b); //echoes b_protected and ba_private
echo '<br />';
$b->print_other($a); //echoes a_protected and a_private
?> 



//把类比作一套抽象的程序, 对象比作一家实体工厂, 按照程序建造一批拥有相同构造的工厂. 拥有相同构造是什么意思呢? 用个比喻, a 和b 都有一间厨房, 这个厨房拥有程序赋予它的全部属性, 厨房的作用在于, 生产一个美女.a公司 和b公司同时就产生了两个美女.对吧?


// 没有常量函数!

//public static function myfunc(){}  和 static public function myfunc() {} 是没有区别的. 


// 不要定义相冲突的属性或方法. 比如: static protected $myvalue ; static private function myfunc(){} ; 这些属相相冲突, protected 和private 属性方法都不能在外部直接调用, 因此在需要在外部直接调用的时候,定义static 没有意义.


// 静态函数?? \ 静态变量支持重载. 常量支持重载.普通变量,普通函数不支持重载.

测验代码:

<?php

class myclass {


	public $name = 'name';
	
	static function show(myclass $object){
	
		return $object->name;
	
	}


}

class onther extends myclass{


	public $name = 'onther';
	
	static function show(myclass $object){
	
		return $object->name;
	
	}


}
$obj = new onther;

echo onther::show($obj);





<?php
class Foo {}
class Bar extends Foo {

   static function test() {
       return(
           array(
               new self,
               new self(),
               new parent( 'a', 1 ),
           )    );
   }
}
   print_r( Bar::test() ); ?>








<?php
class A
{
   protected $x = 'A';
   public function f()
   {
       return '['.$this->x.']';
   }
}

class B extends A
{
   protected $x = 'B';
   public function f()
   {
       return '{'.$this->x.'}';
   }
}

class C extends B
{
   protected $x = 'C';
   public function f()
   {
       return '('.$this->x.')'.parent::f().B::f().A::f();
   }
}

$a = new A();
$b = new B();
$c = new C();

print $a->f().'<br/>';
print $b->f().'<br/>';
print $c->f().'<br/>';
?>



 Undefined "Property" my_static  ??
 静态变量不能这样访问吗 ? print $foo->my_static .


// $Obj  和 $obj  是两个不同的对象. 

//调用方法不能为空. 

//不要被大段大段的代码吓着, 其实他们很亲切, 他们只是想让你明白一个道理而已.

//抽象类方便用于公共属性和方法. 接口类可以实现多继承.






<?php
class A
{
   public function __toArray()
   { // do change to array
   }
}

function insertData(array $array)
{ // insert data into database
}

insertData($a = new A());
?>





<?php


function bool2str($bool)
{
    if ($bool === false) {
        return 'FALSE';
    } else {
        return 'TRUE';
    }
}

function compareObjects(&$o1, &$o2)
{
    echo 'o1 == o2 : ' . bool2str($o1 == $o2) . "\n";
    echo 'o1 != o2 : ' . bool2str($o1 != $o2) . "\n";
    echo 'o1 === o2 : ' . bool2str($o1 === $o2) . "\n";
    echo 'o1 !== o2 : ' . bool2str($o1 !== $o2) . "\n";
}

class Flag
{
    public $flag;

    function Flag($flag = true) {
        $this->flag = $flag;
    }
}

class OtherFlag
{
    public $flag;

    function OtherFlag($flag = true) {
        $this->flag = $flag;
    }
}




/* ... */
$o = new Flag();
$p = new Flag(10);

/* ... */
echo "Two instances of the same class\n";
compareObjects($o, $p);
?>


//  00  和0  相等, 但不全等. 011 和11 不相等也不全等. 

// $obj1 = $obj2 是两者引用地址想等,  $obj1 = clone $obj2 是$obj2 的一个备份.    


<?php


class Connection {
    protected $link;
    private $server, $username, $password, $db;
    
    public function __construct($server, $username, $password, $db)
    {
        $this->server = $server;
        $this->username = $username;
        $this->password = $password;
        $this->db = $db;
        $this->connect();
    }
    
    private function connect()
    {
        $this->link = mysql_connect($this->server, $this->username, $this->password);
        mysql_select_db($this->db, $this->link);
    }
    
    public function __sleep()
    {
        return array($this->server, $this->username, $this->password, $this->db);
    }
    
    public function __wakeup()
    {
        $this->connect();
		return true ;
    }
}

$obj =new Connection('localhost','root','duwoaini00','database_18');
print_r($obj->__sleep());
echo $obj->__wakeup();


?> 





<?
class BaseObject
{
   function __sleep()
   {
       $vars = (array)$this;
       foreach ($vars as $key => $val)
       {
           if (is_null($val))
           {
               unset($vars[$key]);
           }
       }    
       return array_keys($vars);
   }
};
?> 









<?php

class test
{



	private $a;
	static $b = '0';
	
	public function __construct(){
	
		$this->a='test';
		$this->b='baby';
	
	}
	
	function __toString(){
	
		return (string)$this->a;
	
	}
   function __sleep()
   {
       $vars = (array)$this;
       foreach ($vars as $key => $val)
       {
           if (is_null($val))
           {
               unset($vars[$key]);
           }
       }    
       return array_keys($vars);
   }
}


//$obj = new test;
//var_dump($obj->__sleep());

?>


get_class_vars() 函数不能访问 私有成员属性.
get_class_method() 函数不能访问 私有成员方法.