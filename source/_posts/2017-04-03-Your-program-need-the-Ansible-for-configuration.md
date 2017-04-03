---
title: Your program need the Ansible for configuration
date: 2017-04-03 23:28:12
tags:
---

I use Python. I use `python program.py` to run my python script.

But on the server, I use `ansible-playbook playbook.yml` to let code run at the server.

I also use **docker**.

<!--More-->



## Let the code go under Ansible and Docker

**Ansible** is for program's configuration.

**Docker** is for program's environment.

**Example:**

Project: pychpgoods

> In this project, I use Docker and Ansible. Use Ansible to build the Docker image, and run the code by using docker container.

pychpgoods **tree**:

```
➜  /Users/saml/workspace/labs/pychpgoods> git:(refactor) ✗ tree
.
├── Dockerfile
├── LICENSE
├── README.md
├── deploy
│   ├── README.md
│   ├── conf.cfg
│   ├── conf.cfg.bk
│   ├── conf.cfg.example
│   ├── pychpgoods-container.yml
│   ├── sendlist
│   └── simplelog.cfg.example
├── pychpgoods
│   ├── __init__.py
│   ├── core.py
│   ├── courier.py
│   ├── pymail.py
│   ├── resources.py
│   ├── sendedlist.py
│   └── simplelog.py
├── requirements.txt
└── tests
    ├── __init__.py
    ├── __pycache__
    ├── test_core.py
    ├── test_courier.py
    └── test_sendedlist.py

4 directories, 22 files
```
## Docker part

> I want my program run and independent of system environment. So I use docker to build my program environment.

 **Dockerfile**:

```yaml
FROM ansible/ubuntu14.04-ansible:stable
MAINTAINER callsamleung@gmail.com

ADD deploy /srv/deploy
WORKDIR /srv/deploy
ADD pychpgoods /srv/project/pychpgoods
RUN ansible-playbook pychpgoods-container.yml -c local
RUN ln -sf /dev/stdout /srv/deploy/log/pychpgoods.log
CMD ["python", "/srv/project/pychpgoods/core.py"]
```

## Ansible part
> In my program, I need a python config file, cache file and logging config file to let the code go right. I use Ansible help me to copy all that file to the right position.

**Ansible playbook** :

```yaml
---
- hosts: local
  vars:
    project_name: pychpgoods
    project_path: /srv/project/pychpgoods
    deploy_path: /srv/project
    entry_file: /srv/project/pychpgoods/core.py
    log_path: /srv/deploy/log
    sendlist_file: /var/tmp/sendlist
  tasks:
### COPY SOURCE CODE ###
    - name: create log folder
      file:
        path: "{{ log_path }}"
        state: directory
        mode: "u+wrx,g+rx,o+rx"
    - name: copy config
      template:
        src: conf.cfg
        dest: "{{ project_path }}/conf.cfg"
    - name: copy empty sendlist
      copy:
        src: sendlist
        dest: "{{ sendlist_file }}"
        mode: "u+wr,g+wr,g+wr"
    - name: copy empty simplelog cfg
      template:
        src: simplelog.cfg.example
        dest: "{{ project_path }}/simplelog.cfg"
```
After that, use `docker build -t callsamleung/pychpgoods .` than you have a image. use this `docker run callsamleung/pychpgoods` let the code "build" by **Ansible**, and run under **Docker**(container).
