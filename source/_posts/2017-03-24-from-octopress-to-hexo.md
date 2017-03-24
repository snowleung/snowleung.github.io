---
title: from octopress to hexo
date: 2017-03-24 07:36:55
tags:
---

## Hello Hexo

from octopress to hexo, because:

```
when I write, I'm blogger. when I coding, I'm programmer.
```

<!--More-->

## Install

* Follow [offical](https://hexo.io/zh-cn/docs/)

##Migration

* Follow [offical](https://hexo.io/zh-cn/docs/migration.html)

## CNAME

```
copy from [octopress]._source to [hexo]._source
```

also favicon, attachments and you personal page.

## Deploy and Backup

##### Deploy

in _config.yml, sepcify *deploy* section.

```yaml
deploy:
  type: git
  repo: https://github.com/snowleung/snowleung.github.io
  branch: master
```

in command line, just type `hexo generate&&hexo deploy`.

*WRANING*: will take `-f` when git push.

##### Backup

```bash
git init
git checkout -b hexo #use this branch to backup your hexo file.
git remote add origin your_github_url
git push origin hexo:hexo   # your branch:github branch
```

everything is OK.