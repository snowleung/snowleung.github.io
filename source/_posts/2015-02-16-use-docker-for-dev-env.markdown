---
layout: post
title: "Use docker for dev env"
date: 2015-02-16 16:52
comments: true
categories: vagrant
---

### 使用docker去搭建一个简单的开发环境

基于ubuntu14.03lts vagrant box 做的演示

演示所需image

* django:1.7.4 image
* mysql image

首先就是pull images

```
vagrant ssh
sudo -i

docker pull django：1.7.4
```

#### 先做django project

* 在vagrant默认的目录下建一个项目叫hello
* 然后

```
docker run -d -p 8080:8080  -v /vagrant/hello/:/home/ -it django:1.7.4 python /home/manage.py runserver 0.0.0.0:8080
```

* /vagrant/hello 是虚拟机默认挂在宿主机的目录
* /mnt/hello 是docker container里面的目录
* 所以意思就是挂docker container里面的目录到vm的目录(因为vm默认也挂了宿主机的目录，所以省了一步)
* -d deamon模式

```
docker inspect 'your container id'
```

找到ip地址就可以访问了


#### 设定mysql了

```
docker pull mysql
docker run -d -e MYSQL_ROOT_PASSWORD=root -it mysql:latest

```

* 启动一个mysql container之后，就可以用docker inspect 查看他的ip，然后把ip填入django settings.py中

```
docker inspect 'mysql container id'
```


#### 结束

* 首先，用docker做这些事比较合适真实环境中的多个*系统*交互，比如多个web server都要互相交互
* 要理解container， 在这里我觉得Container就是一些个服务(service)的集合
* docker来做这个事感觉很有 运维味
* 上面的过程中可以看到，container之间都是有ip的，而且这个ip在每次container重启的时候都会变，这就使得每次都需要重新设定ip地址，貌似有解决方法，看这里[github](https://github.com/ggtools/docker-tools)
* 所以在没有ddns之前觉得用这个来做开发环境有点累
* 之后补ddns
* 之后补fig工具

