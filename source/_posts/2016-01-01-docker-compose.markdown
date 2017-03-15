---
layout: post
title: "docker compose"
date: 2016-01-01 23:13
comments: true
categories: Program
---

###ENV

http://dockerpool.com/static/books/docker_practice/dockerfile/basic_structure.html

看完上面的链接，已经可以说对docker到底怎么用有了基本知识了。对于开发的运用中，这个已经能够满足

当年在这篇中写了相关的东西，缺少dns和fig

http://www.leisiwo.com/blog/2015/02/16/use-docker-for-dev-env/

如今再次看了一下docker的整个流程，所以有这个笔记

<!--More-->

---

###回答问题：

* DNS

A：我们用DNS问题来解决无需记忆每次容器启动时的ip地址，本质上就是要通过
ip地址找到容器。但是深入思考，访问容器无非两个场景

a) 容器之间访问

b) 非容器之间的访问

```
关于a)，容器之间的访问，其实已经有很好的解决方案就是使用--link参数解决
Document: https://docs.docker.com/engine/reference/commandline/run/#run
使用--link之后，容器之间就可以进行通讯了，而通讯的参数，用的是类似环境
变量的方式
例如如果用mysql，那么就会有MYSQLDB_ROOT_PASS_WORD这样的变量来标注
root的密码，对于python来说os.environ['MYSQLDB_ROOT_PASS_WORD']即可获得
密码。
```

```
关于b)，非容器之间的访问，则只需要在宿主上做好转发即可。（-p参数可以指
定转发端口）我使用的是vbox虚拟机中的环境运行docker，所以物理机
上访问docker容器，只需要固定vbox虚拟机中ip即可。
大概是
container_ip_port:virutalmashine_ip_port --> virtualmashine_ip_port
--> your_macbook_access
```
REFERENCE

【Docker 中的网络功能介绍】http://dockerpool.com/static/books/docker_practice/network/README.html
这里更加系统的说明了上面的事。

* fig

A：请使用docker-compose
【compose file reference】https://docs.docker.com/compose/compose-file/#compose-file-reference

以上回答完毕。

---

###接下来说说其他基础知识

* VOLUMES

【Docker 数据管理】http://dockerpool.com/static/books/docker_practice/data_management/README.html

【volume】 http://dockone.io/article/129 说的非常清晰，推荐

* dockerfile

dockerfile 我认为是一个image commit的集合，所以如果你还在一行一行的
commit，写完之后不妨组合到dockerfile中，下次可以docker build 搞定

---

###其他：

以上仅对docker用于快速搭建开发环境所做的一些思考，不可用于生产。

REFERENCE

【compose Example django】https://docs.docker.com/compose/django/

【docker file reference】https://docs.docker.com/engine/reference/builder/#dockerfile-reference
