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
(看这里吧)[http://www.kafeitu.me/git/2012/03/27/git-submodule.html]


####总结
* 子模块在父项目中只是记录commit_id，也依赖它来执行操作
* submodule 为的就是在父项目中永远只更新子模块内容
* 所以父项目中不要有需要修改子模块内容的*想法*


参考资料
(http://www.kafeitu.me/git/2012/03/27/git-submodule.html)[http://www.kafeitu.me/git/2012/03/27/git-submodule.html]
