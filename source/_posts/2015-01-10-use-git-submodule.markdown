---
layout: post
title: "use git submodule"
date: 2015-01-10 00:16
comments: true
categories: [takeiteasy, git]
---
### 我有一个.emacs文件，如何用submodule去维护其他模块？
#### 如何添加子模块
* git submodule add resp path
* git submodule init
* git submodule update
* git status (这时会看到.submodule和commit_id未提交)
* git commit (保存子模块和子模块的commit_id)

#### 如何更新子模块
* cd 子模块
* git pull origin master ，不能git pull，因为You are not currently on a branch.
* cd .. && git status (这里会看到子模块的commit id更新了)
* git commit (提交子模块更新)

#### 新成员加入开发，如何获取clone项目?
* git clone resp (父)
* git submodule init (子项目没有内容)
* git submodule update （更新到上次提交到父项目的子项目commit_id， 所以如果此时子项目有更新，需要重新走更新子模块的流程）
* 快捷方式:git clone --recursive resp (同时clone所有模块,只到父模块中记录过的commit-id)

#### 如何删除子模块
* 很麻烦
[看这里吧](http://www.kafeitu.me/git/2012/03/27/git-submodule.html)


####总结
* 子模块在父项目中只是记录commit_id，也依赖它来执行操作
* submodule 为的就是在父项目中永远只更新子模块内容
* 所以父项目中不要有需要修改子模块内容的*想法*


[参考资料](http://www.kafeitu.me/git/2012/03/27/git-submodule.html)


UPDATE:

* 尝试过subtree子命令，感觉这个指令更加多的是一种分支管理策略，所以跳不出一个很重要的点就是

```git中对于子模块(子仓库)的管理都需要在父项目中有commit_id来追踪，所以个人觉得最需要的管理就是如何可以让子模块的更新最大限度的减少对父项目的影响```

* 参考资料
* [http://aoxuis.me/posts/2013/08/07/git-subtree/](http://aoxuis.me/posts/2013/08/07/git-subtree/)
* [http://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A0%91%E5%90%88%E5%B9%B6](http://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A0%91%E5%90%88%E5%B9%B6)