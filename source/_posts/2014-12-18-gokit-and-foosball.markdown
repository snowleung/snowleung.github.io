---
layout: post
title: "gokit and foosball"
date: 2014-12-18 12:13
comments: true
categories: takeiteasy
---

###For [Gizwits](http://www.gizwits.com)
####准备
1. [gservice_sdk_py](https://github.com/gizwits/gservice_sdk_py)

####步骤
1. 配置gokit。
   1. 请参考[How To Build Smart FoosBall with GoKit](https://github.com/smartfoosball/foosball-mcu/wiki/How-To-Build-Smart-FoosBall-with-GoKit)
2. 通过机智云获取gokit反馈的数据
   1. 注册成为[机智云](http://www.gizwits.com)的开发者，依照[步骤](https://github.com/smartfoosball/foosball-mcu/wiki/How-To-Build-Smart-FoosBall-with-GoKit#步骤)配置好gokit产品。
   2. 安装[gservice_sdk_py](https://github.com/gizwits/gservice_sdk_py)
   3. 使用机智云注册的gotki产品信息配置gservice_sdk的client，然后调用retrieve_product_histroy_data方法从机智云获取设备数据
   3. 根据retrieve_product_histroy_data返回的数据更新网站的进球数据, 代码：[参考class Command](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/management/commands/goals.py)

===

###For [Wechat](http://weixin.qq.com/)
####准备
1. [wechatpy 0.7.2](https://pypi.python.org/pypi/wechatpy/0.7.2)
2. [enum34 1.0.4](https://pypi.python.org/pypi/enum34/1.0.4)
3. [requests 2.5.0](https://pypi.python.org/pypi/requests/2.5.0)

####步骤
1. 编写wechat_echo代码
   1. [参考class WechatEcho](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/views.py)
2. 启用服务器配置(测试坏境)
   1. 登录[微信sanbox](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login), 扫描二维码并登陆。
   2. 修改接口配置信息如图。
3. 使用OAUTH方式获取微信用户授权。
   1. 依照微信文档[网页授权获取用户基本信息](http://mp.weixin.qq.com/wiki/17/c0f37d5704f0b64713d5d2c37b468d75.html)(共四步, 具体实现可查看[用户同意授权class BaseWeixinView](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/views.py)[拉取用户信息def wechat_oauth2](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/views.py)
4. 使用微信返回用户信息更新数据库内容。