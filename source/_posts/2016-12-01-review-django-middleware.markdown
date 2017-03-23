---
layout: post
title: "Review Django: Middleware"
date: 2016-12-01 15:11
comments: true
categories: Program
---

###What’s Django Middleware###

* 是Django请求、响应处理的一个钩子(Hook)框架，用于全局修改Django的输入或输出。

<!--More-->

###Middleware order and layering###

* 中间件的顺序结构可以考虑为“洋葱”的结构（一层包一层）
* request处理顺序从上到下（遇到response就立即停止），response返回顺序由下到上（遇到Exception就立即停止）

###Writing your own middleware###

* 定义一个Python的类，其中包含以下方法（至少一个）
    * process_request(request)# 在所有request中，并且在Django决定执行哪个view之前，会调用此方法
    * process_view(request, view_func, view_args, view_kwargs) #在Django执行view之前，会调用此方法
    * process_template_response(request, response) # 在view完成执行后、如果response包含render方法，会调用此方法（这表明
    * process_response(request, response) #在所有的response被返回浏览器之前，会调用此方法
    * process_exception(request, exception) #当view执行时引发异常时，会调用此方法

###Code Example###

Forbids access to User-Agents in settings.DISALLOWED_USER_AGENTS

* CommonMiddleware: https://docs.djangoproject.com/en/1.8/_modules/django/middleware/common/#CommonMiddleware


###REFERENCE###

* Middleware (Django document):  https://docs.djangoproject.com/en/1.8/topics/http/middleware/
* Hooking (wiki): https://en.wikipedia.org/wiki/Hooking
* Understanding Django Middlewares(by Akshar Raaj) :http://agiliq.com/blog/2015/07/understanding-django-middlewares/
