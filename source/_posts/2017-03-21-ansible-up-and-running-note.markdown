---
layout: post
title: "ansible up and running note"
date: 2017-03-21 09:33
comments: true
categories: 
---



## What's Ansible

### [Ansible is Simple IT Automation](https://www.ansible.com/)

<!—More—>



## QuickView
> few step to complete.
>

0. less config of ansible([ansible.cfg](http://docs.ansible.com/ansible/intro_configuration.html#getting-the-latest-configuration))
1. decide hosts(your server, connections and everything if your can find the server)
2. generate [Playbook](http://docs.ansible.com/ansible/playbooks.html)
   * play with tasks(support by [Module](http://docs.ansible.com/ansible/modules_by_category.html))
3. execute ansible playbook.
4. get some coffee and wait complete.




## Playbook

> basic config in your playbook wit yaml(syntax).

[Basic](http://docs.ansible.com/ansible/playbooks_intro.html#basics): include `hosts`,`remote_user`,`tasks`.

with `tasks` [section](http://docs.ansible.com/ansible/playbooks_intro.html#tasks-list), use this code to 'play with tasks'

```yaml
tasks:
    - name: test connection
      ping:
      remote_user: yourname
```

##### tips with '[Handlers: Running Operations On Change](http://docs.ansible.com/ansible/playbooks_intro.html#tasks-list)'

> I use it for **restart service** and **restart server**, only.

include `notify` in your `task` like this:

```yaml
- name: template configuration file
  template: src=template.j2 dest=/etc/foo.conf
  notify:
     - restart memcached
     - restart apache
```

AND than add `handlers` section in your **Playbook**:

```yaml
handlers:
    - name: restart memcached
      service: name=memcached state=restarted
    - name: restart apache
      service: name=apache state=restarted
```

full example on ansible [doc](http://docs.ansible.com/ansible/playbooks_intro.html#playbook-language-example).

```yaml
---
- hosts: webservers
  vars:
    http_port: 80
    max_clients: 200
  remote_user: root
  tasks:
  - name: ensure apache is at the latest version
    yum: name=httpd state=latest
  - name: write the apache config file
    template: src=/srv/httpd.j2 dest=/etc/httpd.conf
    notify:
    - restart apache
  - name: ensure apache is running (and enable it at boot)
    service: name=httpd state=started enabled=yes
  handlers:
    - name: restart apache
      service: name=httpd state=restarted
```



## REFERENCE

* [Ansible: Up and Running: Automating Configuration Management and Deployment the Easy Way](https://www.amazon.com/Ansible-Automating-Configuration-Management-Deployment/dp/1491915323/ref=sr_1_1?ie=UTF8&qid=1490059919&sr=8-1&keywords=ansible+up+and+running)

* [Ansible Documentation](http://docs.ansible.com/ansible/index.html)

