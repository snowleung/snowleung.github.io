---
layout: post
title: "python effective cheatsheet 03"
date: 2015-03-09 23:13
comments: true
categories: code,python
---


### 其实是读书猫纸

*  [Effective系列丛书:编写高质量代码:改善Python程序的91个建议](http://www.amazon.cn/Effective%E7%B3%BB%E5%88%97%E4%B8%9B%E4%B9%A6-%E7%BC%96%E5%86%99%E9%AB%98%E8%B4%A8%E9%87%8F%E4%BB%A3%E7%A0%81-%E6%94%B9%E5%96%84Python%E7%A8%8B%E5%BA%8F%E7%9A%8491%E4%B8%AA%E5%BB%BA%E8%AE%AE-%E5%BC%A0%E9%A2%96/dp/B00KYFJTP8/ref=sr_1_1?ie=UTF8&qid=1425914107&sr=8-1&keywords=%E6%94%B9%E5%96%84python)


### 03

* import, 会生成pyc文件， 不会循环引用；from xxx import xxx， 会命名空间冲突，会循环引用； import 会编译和新建一个对象到sys.modules中
* 优先使用absoult import，而不是from .. import xx
* ++i == +(+)i，不是自增
* with syntax, 上下文管理器、协议
* try, except, else, while else, for else
* 捕获异常原则，精确、有序、易读
* finally中return 会令函数提前返回
* string: more join, less +，字符串内存不可变相关
* more format(), less %
* 对象的id, type, value，可变对象和不可变对象
* 列表解析：
```
[expr for iter_item in iterable if cond_expr ], list
(expr for iter_item in iterable if cond_expr), tuple
{expr for iter_item in iterable if cond_expr}, set
{expr1, expr2 for iter_item in iterable if cond_expr}, dict

```
* 传参数， 传的是对象。
```
共享可变对象的内存地址
不可变对象的操作则重新分配

```

* 使用None做可变参数
* 慎用可变参数
```
*args (a,b,c,...)
**kwargs k1=v1, k2=v2, k3=v3
装饰器
参数不确定
class中的多态
```

* str -- 普通用户， repr -- 开发者, 可配合eval()
* @classmethod, @staticmethod
```
@classmethod 多态，类变量互相独立
@staticmethod 方便用类组织代码
```