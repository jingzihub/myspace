---
layout: post
title: "简单的oop知识"
date: 2013-11-19 23:00:00
category: blog
description: "简单的oop知识"
---
新手练习的一个类 高手免进
学了PHP快3个月了  还是一只小菜鸟 现在写个类 跟菜鸟朋友一起研究
高手就不用进来看了 呵呵  因为漏洞很多
这个类是数据库连接类 支持oracle+mysql+mssql (虽然写这个类根本就没意义 不过也算是个类)
功能不多 但是能上手  如果你刚刚在学习类
可以完善这个类的  因为我就简单写了几个代码 应该你能看懂的

首先是类的主文件

db.class.php
复制PHP内容到剪贴板
PHP代码:

<?php
 /*
  *--------------------------------
  * 文件 : 多功能数据库操作
  * 功能 : 数据库连接 Oracle+Mysql+Mssql
  * 日期 : 2009-1-10
  *
  *    BY: 我是坏人
  * Email: [email=baddie@126.com]baddie@126.com[/email]
  * 注意: 这个版本只是演示版本,没多少功能.非商业代码,欢迎转载使用及修改.
  *    但如果发现问题或者想需要更多功能,请联系我,我好修改.
  *  
  *    由于我电脑没装oracle,并对它不是很懂,再加上oracle的sql语句差别.所以oracle这块肯定有问题.
  *    请使用oracle数据库的朋友使用后联系我,我好改正..
  *--------------------------------
  */
  
  final class db {
 
  private $dbtype = ""; 
  private $dbhost = "";
  private $dbuser = "";
  private $dbpass = "";
  private $dbdata = "";
  private $dbcode = "";
  private $conn = "";
  
  function __construct($dbtype,$dbhost,$dbuser,$dbpass,$dbdata,$dbcode) {
   
   $this->dbtype = $dbtype;
   $this->dbhost = $dbhost;
   $this->dbuser = $dbuser;
   $this->dbpass = $dbpass;
   $this->dbdata = $dbdata;
   $this->dbcode = $dbcode;
   $this->Connect();
   }
  
  function Connect() {
   
   // Oracle 数据库连接
   if($this->dbtype == "oracle") {
    if($this->dbhost == "localhost") {
     $this->conn = @oci_connect("$this->dbuser","$this->dbpass","$this->dbdata") or die(' Oracle 服务器连接失败<br>原因:'.$this->error());
     } else {
      die("下一个版本将支持远程oracle服务器");
      }
    }    
   // Mysql 数据库连接
   elseif($this->dbtype == "mysql") {
    $this->conn = @mysql_connect("$this->dbhost","$this->dbuser","$this->dbpass") or die(' MySQL 服务器连接失败<br>原因:'.$this->error());
    @mysql_select_db("$this->dbdata",$this->conn) or die(' MySQL 数据库连接失败<br>原因:'.$this->error());
    @mysql_query("set names $this->dbcode");    
    }  
   // Mssql 数据库连接
   elseif($this->dbtype == "mssql") {
    $this->conn = @mssql_connect("$this->dbhost","$this->dbuser","$this->dbpass") or die(' MsSQL 服务器连接失败<br>原因:'.$this->error());
    @mssql_select_db("$this->dbdata",$this->conn) or die(' MsSQL 数据库连接失败<br>原因:'.$this->error()); 
    }
   
   }
  
  
  //删除数据库表函数  使用方法: $db->drop("baddie");
  function drop($table) {
     
   $sql = "drop table if exists $table";
   $this->query($sql);  
      
   }
   
   
  //创建数据库表函数   使用方法: $db->create("baddie(id int,name varchar(20))");
  function create($table) {
   
   $sql = "create table if not exists $table";
   $this->query($sql);
    
   }
  
  
  //数据库insert函数   使用方法: $db->insert("baddie","id","2");
  function insert($table,$field,$value) {  
   
   $sql = "insert into $table($field) values ($value)";
   $this->query($sql);
    
   }
   
  
  //数据库update函数   使用方法: $db->update("baddie","name","admin","id","1");
  function update($table,$field,$value,$condition,$key) {  
   
   $sql = "update $table set $field=$value where $condition=$key";
   $this->query($sql);
    
   }
  
  
  //数据库delete函数   使用方法: $db->del("baddie","id","1");
  function del($table,$condition,$key) {  
   
   $sql = "delete from $table where $condition=$key";
   $this->query($sql);
    
   } 
   
   
  //数据库追加删除字段函数
  //追加字段使用方法: $db->addfield("baddie","name VARCHAR(100) NOT NULL");
  //删除字段使用方法: $db->delfield("table","name");
  function addfield($table,$fiele) {  
   $sql = "alter table $table add $field";
   $this->query($sql); 
   } 
  function delfield($table,$field) {  
   $sql = "alter table $table drop $field";
   $this->query($sql); 
   }
  
  
  // 数据库查询函数 query():返回一个布尔类型 true or false 如果出错 则返回错误信息
  // 使用方法: $res = $db->query("select * from table where id=1");
  function query($sql) {
   
   $arr = array('SELECT','SHOW','EXPLAIN','DESCRIBE');  //mysql对select返回的是资源 所以这里判断
   $check = explode(' ',$sql);
     
   if($this->dbtype == "oracle") {
    if(!oci_execute(oci_parse($this->conn,$sql))) {
     echo $this->error();
     }
    }     
   elseif($this->dbtype == "mysql") {
    if(in_array(strtoupper($check[0]),$arr)) {
     return @mysql_query($sql);
     } else {
      if(@mysql_query($sql)) {
       return true;
       } else echo $this->error();
      }
    }     
   elseif($this->dbtype == "mssql") {
    if(!mssql_query($sql)) {
     echo $this->error();
     }
    } 
   
   }

  // 数据库返回函数 num_rows(): 返回一个整数  取得结果集中行的数目
  function num_rows($res) {
   
   if($this->dbtype == "oracle") {
    return oci_num_fields($res);
    }    
   elseif($this->dbtype == "mysql") {
    return mysql_num_rows($res);
    }    
   elseif($this->dbtype == "mssql") {
    return mssql_num_rows($res);
    } 
   
   }
  
  
  // 数据库返回函数 fetch_array(): 返回一个数组集合
  function fetch_array($res) {
   
   if($this->dbtype == "oracle") {
    return oci_fetch_array($res);
    }    
   elseif($this->dbtype == "mysql") {
    return mysql_fetch_array($res);
    }    
   elseif($this->dbtype == "mssql") {
    return mssql_fetch_array($res);
    } 
   
   }
 
 
  // 数据库返回函数 fetch_object(): 返回一个对象集合
  function fetch_object($res) {
   
   if($this->dbtype == "oracle") {
    return oci_fetch_object($res);
    }  
   elseif($this->dbtype == "mysql") {
    return mysql_fetch_object($res);
    }   
   elseif($this->dbtype == "mssql") {
     return mssql_fetch_object($res);
    } 
   
   }
    
  
  // 数据库出错显示
  function error() {
   
   if($this->dbtype == "oracle") {
    return oci_error();
    exit;
    }
   elseif($this->dbtype == "mysql") {
    return mysql_error();
    exit;
    }
   elseif($this->dbtype == "mssql") {
    return mysql_error();
    exit;
    }
   
   }
   
  
  // 数据库关闭函数 
  function close() {
   
   if($this->dbtype == "oracle") {
    oci_close($this->conn);
    }  
   elseif($this->dbtype == "mysql") {
    mysql_close($this->conn);
    }  
   elseif($this->dbtype == "mssql") {
    mssql_close($this->conn);
    } 
   
   }
   
  
  // 稀构函数
  function __destruct() {
   
   $this->close(); 
   $this->conn = null;
    
   }
  
  }
?>

接着是数据库连接文件

conn.php
复制PHP内容到剪贴板
PHP代码:

<?php
 /*
  *--------------------------------
  * 文件 : 数据库连接文件
  * 
  * 
  *    BY: 我是坏人
  * Email: [email=baddie@126.com]baddie@126.com[/email]
  *--------------------------------
  */
    function __autoload($classname) {
       include_once $classname.'.class.php';
       }
  
  $dbtype = "mysql";              //定义数据库类型  可选 : mysql,mssql,oracle
  $dbhost = "localhost";      //定义数据库服务器IP
  $dbuser = "test";        //定义数据库用户名
  $dbpass = "123456";       //定义数据库密码
  $dbdata = "temp";        //定义数据库
  $dbcode = "utf-8";        //定义数据库编码,请保持数据库编码与代码编码相同 目前仅支持MYSQL
  
  $db = new db($dbtype,$dbhost,$dbuser,$dbpass,$dbdata,$dbcode);    //实例化对象
?>
