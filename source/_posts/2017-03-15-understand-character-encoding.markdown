---
layout: post
title: "Understand_Character_encoding"
date: 2017-03-15 11:20
comments: true
categories: 
---

# 弄清字符编码和它的编码方式

计算机中，用0和1来作为最小单位，**意义**是假或真，用一定数量的0和1组合来描述世界，一定数量组合的内容足够多时，我们就可以称之为语言。

同样，在中文里，每一个中文字就是一个最小单位，每一个最小单位都有自己的**意义** ，数量足够多后，同样也称为语言。



## 基础概念

* *字符*（[Character](https://en.wikipedia.org/wiki/Character_(computing))），在计算机中就是一个信息的最小载体。对于中文的则可以叫[字素](https://zh.wikipedia.org/wiki/%E5%AD%97%E4%BD%8D)，所以a，b，你，我，都代表一个*字符*。
* UTF（Unicode Transformation Format）：Unicode转换格式
* Byte：字节、位元组（港澳台）；Bit：比特、位元（港澳台）；1 Byte = 8 bit





## 字符编码（字符集）

对于**字符编码**这四个字，我理解为**语言**，和上面的语言一样，而计算机的语言，也可以理解为计算机的字符编码（字符集）。如果字符编码更难理解，可以参看[字符编码](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81)的维基百科。如果还是很难理解，则可以想象为

* 字符编码（字符集）是
* 字符
* 通过编码
* 的方式
* 被识别
* 的过程

相当于：f(x)=y 中


* f(x)=y（字符编码（字符集））是
* x（字符）
* 通过f()（编码）
* 的f(x)（方式）
* 与y对应（被识别）
* 的过程


**虽然不严谨，但是不妨记忆**。

至于为什么可以字符编码可以同义为字符集，[wiki](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81)中的简单字符集是这么说的

> 按照惯例，人们认为字符集和字符编码是[同义词](https://zh.wikipedia.org/wiki/%E5%90%8C%E4%B9%89%E8%AF%8D)，因为使用同样的标准来定义提供什么字符并且这些字符如何编码到一系列的代码单元（通常一个字符一个单元）。由于历史的原因，[MIME](https://zh.wikipedia.org/wiki/MIME)和使用这种编码的系统使用术语**字符集**来表示用于将一组字符编码成一系列八位字节数据的整个系统。

大概是f(x)=y可以称为*函数*一样吧



##ASCII和它的编码方式

[ASCII](https://zh.wikipedia.org/wiki/ASCII)是：

> **ASCII**（发音： [/ˈæski/](https://zh.wikipedia.org/wiki/Help:%E8%8B%B1%E8%AA%9E%E5%9C%8B%E9%9A%9B%E9%9F%B3%E6%A8%99) [**\*ass**-kee*](https://zh.wikipedia.org/wiki/Wikipedia:%E7%99%BC%E9%9F%B3%E9%87%8D%E6%8B%BC)[[1\]](https://zh.wikipedia.org/wiki/ASCII#cite_note-1)，**A**merican **S**tandard **C**ode for **I**nformation **I**nterchange，**美国信息交换标准代码**）是基于[拉丁字母](https://zh.wikipedia.org/wiki/%E6%8B%89%E4%B8%81%E5%AD%97%E6%AF%8D)的一套[电脑](https://zh.wikipedia.org/wiki/%E7%94%B5%E8%84%91)[编码](https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A0%81)系统。它主要用于显示[现代英语](https://zh.wikipedia.org/wiki/%E7%8F%BE%E4%BB%A3%E8%8B%B1%E8%AA%9E)，而其扩展版本[EASCII](https://zh.wikipedia.org/wiki/EASCII)则可以部分支持其他[西欧](https://zh.wikipedia.org/wiki/%E8%A5%BF%E6%AC%A7)[语言](https://zh.wikipedia.org/wiki/%E8%AF%AD%E8%A8%80)，并等同于国际标准**ISO/IEC 646**。

它定义了127个字符

它的编码方式是：

> 使用7位（bits）表示一个字符，共128字符；



## Unicode和它的编码方式（方案）

Unicode没有说字符集来修饰是因为unicode本身就是字符集的意思，可以表述为**统一码（字符集）**，由[UCS](http://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E5%AD%97%E7%AC%A6%E9%9B%86)的标准发展而来。



**它的编码**(UTF)方式（方案）：有UTF-8, UTF-16, UTF-32

其中UTF-8是可变长的编码方式：

> 1. 对于单字节的符号，字节的第一位设为0，后面7位为这个符号的unicode码。
> 2. 对于n字节的符号（1<n<5），第一个字节的前n位都设为1，第n+1位设为0，后面字节的前两位一律设为10。剩下的没有提及的二进制位，全部为这个符号的unicode码。



## GBxxx和它的编码方式

中国国家标准总局发布的是GB 2312，所以用这个来简述中文编码。

包含6763个汉字*字符*

编码方式：

> 每个汉字及符号以两个[字节](https://zh.wikipedia.org/wiki/%E5%AD%97%E8%8A%82)来表示。第一个字节称为“高位字节”，第二个字节称为“低位字节”。

PS：汉字和符号均是*字符*的意思



## 总结

* ASCII，GBxxx等（[查看更多](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81#.E5.AD.97.E7.AC.A6.E7.BC.96.E7.A0.81.EF.BC.88.E4.B8.8D.E5.85.A8.EF.BC.89)）
  * 它们既是字符集（字符编码），也有自己的编码方式。

* Unicode是全球统一的字符编码（字符集/字符编码）
  * 目标是：全世界的字符都能在Unicode找到
  * UTF-8，UTF16，UTF32都是Unicode的编码方式（用各自的方法实现Unicode）
* 以下用故事来说说

> 在2333年的某一天，我遇到一个人，脑子里就想给他打招呼。于是我脑子里就有了一个`'你好'的想法`。我跑过去，`用中文的方式`对着他喊：你好啊。他一脸萌比，看起来他听不懂中文，于是我`用英文的方式`再喊一次：Hello!然后他对着我傻笑，看起来似懂非懂。最后我`用额头碰了碰他的额头的方式`传送了`'你好'的想法`给他，他终于懂了。
>

* `'你好'的想法`：Unicode
* `用中文的方式`：
  * 用：以GB2312编码方式
  * 中文：GB2312
* `用英文的方式`：
  * 用：以ASCII编码方式
  * 英文：ASCII
* `用额头碰了碰他的额头的方式`：可能是UTF-8或其它编码方式




## 资料链接

[人机交互之字符编码](http://selfboot.cn/2014/08/28/character_encoding/)

[字符编码笔记：ASCII，Unicode和UTF-8](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)

[字符集和字符编码（Charset & Encoding）](http://www.cnblogs.com/skynet/archive/2011/05/03/2035105.html)

[汉字内码扩展规范](https://zh.wikipedia.org/wiki/%E6%B1%89%E5%AD%97%E5%86%85%E7%A0%81%E6%89%A9%E5%B1%95%E8%A7%84%E8%8C%83)

[GB 2312](https://zh.wikipedia.org/wiki/GB_2312)

[字符编码](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81)

[Unicode](https://zh.wikipedia.org/wiki/Unicode)
