---
layout: post
title: "ansible and vagrant provision"
date: 2014-09-17 16:47
comments: true
categories: [code,vagrant]
---

使用python开发Web app，所以总是想有一个自动化部署的开发环境。

####想要自动部署的列表:

* base on vitrual box.(ubuntu 13.04)
* mysql  
* python (include web framework and other package.)  
* install and configure automic on virtualbox.

####Vagrant file setting

* private network  
`config.vm.network "private_network", ip: "192.168.33.33"`  
**可以在直接访问192.168.33.33来访问vbox, 不用做forwarded_port.**  
* provision setting
```
config.vm.provision "ansible" do |ansible|
     ansible.playbook = "ansible/site.yml"
     ansible.verbose = 'vvvv'
     ansible.sudo = true
end
```
使用ansible来作为provision  
指定playbook  
指定显示详细信息  
指定使用sudo执行  
**更多参数请看[这里](http://docs.vagrantup.com/v2/provisioning/ansible.html)**

####ansible

* playbook:[YAML语法](http://zh.wikipedia.org/zh-cn/YAML)  
* intro to playbook:[here](http://docs.ansible.com/playbooks_intro.html)  
* use playbook roles:[here](http://docs.ansible.com/playbooks_roles.html#roles)    
**注意行 This designates the following behaviors, for each role ‘x’:  **  
* module on tasks:[here](http://docs.ansible.com/list_of_commands_modules.html)

###其他

vagrant detail see [this](http://www.vagrantup.com)  
ansible detail see [this](http://www.ansible.com/home), doc see [this](http://docs.ansible.com)  
