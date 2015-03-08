---
layout: post
title: "using git tags"
date: 2015-03-08 18:05
comments: true
categories: [code, git]
---

### 想用版本去规范一下自己写的程序

google 了一下软件版本号规范、风格、规则，也没找到什么好网页，所以还是觉得按自己的想法好了。

约定：

* init版本为0.1.0
* 每次小阶段开发就增加尾号，小阶段暂时为： bugfix、refactor
* 增加一些重要的更新时，中间版本号为1，尾号重置为0
* 看起来第一个0永远都达不到啊【碎碎念】
* 在readme.md上增加一个changelog节，写明小阶段开发的change

### 使用git tag去写版本的部分

* 增加

```
git tag -a tag_name

git push origin tag_name 	#远端增加

```


* 修改， 看起来这个打标签是比较慎重的行为，写错了只能删除。

* 删除

```
git tag -d tag_name

```

* 远端删除

```
git push origin :/refs/tags/tag_name

```


ref: 

* [[Git] 版本控制: 如何使用標籤(Tag)](http://blog.wu-boy.com/2010/11/git-%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6-%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8%E6%A8%99%E7%B1%A4tag/)

* [2.6 Git 基础 - 打标签](http://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)
