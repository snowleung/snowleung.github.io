---
layout: post
title: "Python Code Encodings"
date: 2017-03-16 10:59
comments: true
categories: 
---

Python2的编码问题，老生畅谈
<!--More-->

##Python2.x的str

**str**对象和**unicode**对象同样可以表示字符串([5.6. Sequence Types](https://docs.python.org/2/library/stdtypes.html#sequence-types-str-unicode-list-tuple-bytearray-buffer-xrange))，所以它们应该有相同的操作方式([5.6.1. String Methods](https://docs.python.org/2/library/stdtypes.html#string-methods))。

可是，str并不是真正的字符串，它是字节串。所以如果用str类型来保存中文的话，会得到len('a啊')是4的结果：

```python
Python 2.7.13 (default, Dec 17 2016, 23:03:43)
[GCC 4.2.1 Compatible Apple LLVM 8.0.0 (clang-800.0.42.1)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> test = 'a啊'
>>> len(test)
4
```

在这个过程中，Python隐式编码方式转换了‘啊'这个字，然后保存到test中。

这个隐式编码方式到底是什么，这是由**系统locale決定**的。

```python
Python 2.7.13 (default, Dec 17 2016, 23:03:43)
[GCC 4.2.1 Compatible Apple LLVM 8.0.0 (clang-800.0.42.1)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import locale
>>> locale.getdefaultlocale()
('zh_CN', 'UTF-8')
```

所以，就有以下过程

> 你输入的—>Python转一下—>保存到str中

有了这个过程，在`Python转一下`的时候，如果转不了（比如你输入的是中文，Python用ASCII来转一下），就会引发出**UnicodeEncodeError**或**UnicodeDecodeError** 的问题了。



## Python2.x的Unicode

Python支持Unicode，把

> 你输入的—>Python转一下—>保存到str中

这个过程改为

> 你输入的是Unicode-->Python转一下—>保存到str中

那么，几乎就不会出错了。在Python中，把u放在str前面，就代表你输入的用Unicode来保存。Python操作就少很多以下的误会

误会1，字符串长度:

```python
>>> test = '你好'
>>> len(test)#正确的应该是2
6
```

误会2，字符串截取:

```python
>>> test = '你好'
>>> print test[0]
�
```

以上都是因为没有使用Unicode来保存字符串。



## 更多的decode和encode问题

Python中编码问题，本质上是

> 你要操作一个字符串，Python把你要的字符串拿出来包装一下，给你操作

其中，**Python把你要的字符串拿出来包装一下**就是坑的所在。

### decode

> 将str类型转为unicode类型

### encode

> 将unicode类型转为str类型

以下例子运用decode来说明

```python
>>> test = '好'
>>> test.decode('gb2312')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeDecodeError: 'gb2312' codec can't decode byte 0xbd in position 2: incomplete multibyte sequence
```

**失败**。因为test是用locale指定的方式进行编码的（隐式），所以也需要用locale的指定的方式解码。

```python
>>> test = '好'
>>> test.decode('utf-8')
u'\u597d'
```

**成功**

以下例子说明decode

```python
>>> test = u'好'
>>> test.encode('utf-8')
'\xe5\xa5\xbd'
>>> test.encode('gbk')
'\xba\xc3'
>>> test.encode('gb2312')
'\xba\xc3'
```

**成功**，因为你原来的字符串就是unicode，所以你可以用任何支持的编码方式来对unicode进行编码，得到str对象。



## 隐式编码和解码

正常的操作

* str + str，返回的是str；unicode+unicode，返回的是unicode

```python
>>> 'a' + 'b'
'ab'
>>> u'a' + u'b'
u'ab'
```

演示隐式操作

* str + unicode，返回的是unicode；隐式地str**解码**为unicode，再＋

```python
>>> 'a' + u'b'
u'ab'
```

* str操作，两次操作，都是相同的错误；隐式地unicode**编码**为acii（但是失败了，再str。

```python
>>> str(u'你')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeEncodeError: 'ascii' codec can't encode character u'\u4f60' in position 0: ordinal not in range(128)
>>>
>>> str(u'你'.encode('ascii'))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeEncodeError: 'ascii' codec can't encode character u'\u4f60' in position 0: ordinal not in range(128)
>>>
```



## 还有什么没提到

###### Q：为什么在Python代码中，能看见下面的声明

```python
# -*- coding: <encoding name> -*-
```

A：[PEP 263 -- Defining Python Source Code Encodings](https://www.python.org/dev/peps/pep-0263/)

###### Q：为什么互联网（HTML）推荐UTF-8？

A：因为UTF-8的编码方式，非常特别，[它可以使用1~4个字节表示一个符号，根据不同的符号而变化字节长度](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)。可以达到节省带宽和存储空间的效果

######Q：如果我用Python3的话，还有这些编码问题么？

A：朋友，Python3里面，几乎没了上面的所有问题。看看Python作者Guido van Rossum在2007年写的What’s New In Python 3.0中的[Text Vs. Data Instead Of Unicode Vs. 8-bit](https://docs.python.org/3/whatsnew/3.0.html#text-vs-data-instead-of-unicode-vs-8-bit)：

> Everything you thought you knew about binary data and Unicode has changed


##### 其它资源


* [Python2.x 字符编码终极指南](http://selfboot.cn/2016/12/28/py_encode_decode/)
* [立即停止使用 setdefaultencoding('utf-8')， 以及为什么](http://blog.ernest.me/post/python-setdefaultencoding-unicode-bytes)
* [Solving Unicode Problems in Python 2.7](https://www.azavea.com/blog/2014/03/24/solving-unicode-problems-in-python-2-7/)
* [Unicode HOWTO](https://docs.python.org/2/howto/unicode.html)
* [Python2字符串编码问题总结](http://zhangbohun.github.io/2016/05/29/Python2%E5%AD%97%E7%AC%A6%E4%B8%B2%E7%BC%96%E7%A0%81%E9%97%AE%E9%A2%98%E6%80%BB%E7%BB%93/)
* [Unicode](https://zh.wikipedia.org/wiki/Unicode)
