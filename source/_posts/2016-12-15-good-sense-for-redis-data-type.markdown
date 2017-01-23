---
layout: post
title: "Good Sense For Redis Data Type"
date: 2016-12-15 19:01
comments: true
categories: Program
---

###Redis

* Redis is an open source (BSD licensed), in-memory data structure
  store, used as a database, cache and message broker.

###给妹子说的DataType

Redis支持Strings, Lists, Sets, Hashes, Sorted sets, Bitmaps and
HyperLogLogs数种数据结构。下面就给妹子讲解前五种（Strings, Lists,
Sets, Hashes, Sorted sets,）

####Strings(String)

* String，大家都叫他字符串。字符串意思是字符＋串，字符就是类似a,b,c,d等
等的，串就是把他们组合在一起（如abcd）；正如吉他谱，如果把Redis比喻为一首吉他曲子，弦（Bm，C）＋谱（拨弦）为一个小节，
多个小节组成的Strings，就可以奏响Redis这首曲子了。所以Redis中的String，
就是__键为和弦，值为谱__的这种结构。

####Lists(List)

* List，大家都叫他列表。如果Redis是一个卖糖葫芦串的商人，那么每一个List就是他手
中用竹签穿起山楂来的一个串。那Redis中的List，就是__键为竹签，值为山楂__的这种结构

####Sets(Set)

* Set，大家都叫他集合。集合相当于一个容器，包含在容器里面的“东西”可以叫
为“元素”；元素与元素之间并__无顺序__，并且各个元素是
__不重复__的。如果Redis是一个生果礼品店，那么每一个Set就
是他包装好的生果篮，生果篮里面的生果都放在一起，没有先后顺序，而且同一
种生果不应该多于一个（只有一个苹果，不能两个）。所以，Redis中的Set，就
是__键为生果篮，值为生果（不重复）__的结构。

####Hashes(Hash)

* Hash，可以叫他为哈希表。中学的时候学过f(x)=y，表述为当x一定时，通过
f(x)总会得到y，而哈希表就是用来表达这个思维过程的。如果Redis是一家蔬菜
店，那么每一个hash就是__一个菜类__和__与之对应的价钱__的表格。所以，在
Redis中的Hash，就是__键为菜类，值为对应的价钱__的结构。

#### Sorted Sets

* 已排序的集合，回忆之前Sets，提及__无顺序__，那么，这个Sorted Sets就是__有
顺序__的。比如我们将生果篮里面的生果，按体积大小来做区分的话，就可以得
到一个顺序，比如西瓜最大，到菠萝，到苹果，到草莓这么一个顺序，那原本无
序的生果篮，就变成有顺序的了。所以，Redis中的Sorted Set，就是__键为生
果篮，值为生果（不重复）与体积大小（可排序）__的结构。


###REFERENCE:

* [Data types(Redis)](https://redis.io/topics/data-types)
* [An introduction to Redis data types and abstractions](https://redis.io/topics/data-types-intro)
* [Key-value database](https://en.wikipedia.org/wiki/Key-value_database)
* [Hash table](https://en.wikipedia.org/wiki/Hash_table)
