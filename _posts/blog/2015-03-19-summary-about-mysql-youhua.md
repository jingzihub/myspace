---
layout: post
title: "mysql优化"
date: 2015-03-19 23:00:00
category: blog
description: "mysql优化"
---
##避免在列上直接运算
```
    select * from t where YEARdate: 2015-03-19 11:47:12 >= 2011
```
优化为
```
    select * from t where d >= '2011-01-01'
```
##以小结果集驱动大结果集,把复杂的查询拆分成多个Query

##尽量避免使用LIKE模糊查询

##仅列出需要查询的字段
```
    select * from Member
```
优化为
```
    select id,name,pwd from Member
```
##使用批量插入语句,节省交互

##Limit的基数较大时使用Between,在取比较后面的数据时,先用desc排序后再反向查找

##不使用rand函数来获取随机记录

##避免使用NULL

##不做无谓的排序,尽可能在索引中完成排序

##用count(*)替代count(id)