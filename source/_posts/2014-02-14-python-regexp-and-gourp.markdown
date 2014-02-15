---
layout: post
title: "python regexp and gourp"
date: 2014-02-14 18:07
comments: true
categories: code, reading
---


#####Why you can see this post

One day, a guy want the use regexp to match the ed2k link with python, so he get a pattern from google.


```
pattern : ed2k:\/\/\|file\|[^\|]+\|\d+\|[0-9a-z]+\|(h=[a-z0-9]+\|)?\/
```


It work similar

```
ed2k://|file|!%20(%20NEW%20)%20!%20sod%20japan%20-%20[silk%20labo]%20Love%20Switch%20-%20Another%20Stories%20[SLK20]%20(2%20098%20969%20424).mp4|2098969424|438D794BB3571342F8CFA902681A901C|h=5DUPHBUN52JPTRMLBFTN2SYMFNP3KCS4|/
```
	
but fail at this

```
ed2k://|file|[nowys.org]SILK.LABO.东京恋爱模様.TOKYO.LOVERS.LIFE.01(ED2000.COM).mp4|882032017|6DF424D13F8D7D9DCA1F9A31E0DE3EF6|/
```

after the guy know why, this post upload.

#####So why ?

1 Day: 

* The guy find this [python re模块的findall方法](http://www.douban.com/group/topic/32245600/) and modify the pattern like this:


```
pattern : ed2k:\/\/\|file\|[^\|]+\|\d+\|[0-9a-z]+\|(?:h=[a-z0-9]+\|)?\/
```
	
* It work.

2-3 Day:

* The guy why know why, so he find this book [精通正则表达式](http://www.amazon.cn/精通正则表达式-杰佛瑞E-F-佛瑞德/dp/B008UCHA58/ref=sr_1_1?ie=UTF8&qid=1392373797&sr=8-1&keywords=精通正则表达式) and read chapter 1.

* At chapter 1, the guy know many about **[] () . + * ?** and little **UNICODE** knowledge.

4 day:

* In [LOL](http://leagueoflegends.com)

5 day: 

* The guy finish reading but only at 
chapter 4 and know something about **group**. With that knowledge, the guy want to use regex and do something with this "aaabcbbbbccc" and return "aaa,bbb,ccc".

* So he use that pattern 

```
pattern : "([a-z])\1{2}"
```
		
* that pattern not work at python re.findall()! just output

```
output : ['a','b','c']
```
		
* so he find something about re.match, re.search, re.findall with google, and finally the output get right with this pattern

```
pattern : "(([a-z])\2{2})"
```

* why? See more "**()**" and **group** with this article:

* [【整理】Python中的re.search和re.findall之间的区别和联系 + re.finall中带命名的组，不带命名的组，非捕获的组，没有分组四种类型之间的区别](http://www.crifan.com/python_re_search_vs_re_findall/)
* [Python中re(正则表达式)模块学习](http://www.cnblogs.com/sevenyuan/archive/2010/12/06/1898075.html)
* [python re模块的findall方法](http://www.douban.com/group/topic/32245600/)
* source code for gist: [re_exm](https://gist.github.com/snowleung/9000098)

