---
layout: post
title: "gokit and foosball"
date: 2014-12-18 12:13
comments: true
categories: takeiteasy
---

#概述
基于Python语言进行开发，并使用了Django框架

#For [Gizwits](http://www.gizwits.com)
##依赖的安装包
* [gservice_sdk_py](https://github.com/gizwits/gservice_sdk_py)

##步骤
###配置gokit。
* 请参考[How To Build Smart FoosBall with GoKit](https://github.com/smartfoosball/foosball-mcu/wiki/How-To-Build-Smart-FoosBall-with-GoKit)

###通过机智云获取gokit反馈的数据
* 注册成为[机智云](http://www.gizwits.com)的开发者，依照[步骤](https://github.com/smartfoosball/foosball-mcu/wiki/How-To-Build-Smart-FoosBall-with-GoKit#步骤)配置好gokit产品。
* 安装[gservice_sdk_py](https://github.com/gizwits/gservice_sdk_py)
* 使用机智云注册的gotki产品信息配置**gservice_sdk**的client，然后调用**retrieve_product_histroy_data**方法从机智云获取设备数据。
* 根据**retrieve_product_histroy_data**返回的数据更新网站的进球数据, 代码：[Command](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/management/commands/goals.py)
APPID和PRODUCK_KEY的获取如下图：
  ![app_id_pk](/images/app_id_pkey.png)
  关键代码如下:

```
gsc = GServiceClient(settings.GW_APPID)
ts  = 0
d_team = {'red': 1, 'blue': 2}
d_position = {'red_van': 1, 'red_rear': 2, 'blue_van': 3, 'blue_rear': 4}
while True:
    try:
        game = Game.objects.filter(status=Game.Status.playing.value).first()
        data = gsc.retrieve_product_histroy_data(settings.PRODUCT_KEY, start_ts=ts, limit=10).json()['data']
```

#For [Wechat](http://weixin.qq.com/)
##依赖的安装包
* [wechatpy 0.7.2](https://pypi.python.org/pypi/wechatpy/0.7.2)
* [enum34 1.0.4](https://pypi.python.org/pypi/enum34/1.0.4)
* [requests 2.5.0](https://pypi.python.org/pypi/requests/2.5.0)

##步骤
###编写wechat_echo代码, [WechatEcho](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/views.py)部份代碼如下：
```
class WechatEcho(View):

    def get(self, request):
        signature = request.GET.get('signature', '')
        timestamp = request.GET.get('timestamp', '')
        nonce = request.GET.get('nonce', '')
        echo_str = request.GET.get('echostr', '')

        try:
            check_signature(TOKEN, signature, timestamp, nonce)
        except InvalidSignatureException:
            return HttpResponse(status=403)
        return HttpResponse(echo_str)

    def post(self, request):
        signature = request.GET.get('signature', '')
        timestamp = request.GET.get('timestamp', '')
        nonce = request.GET.get('nonce', '')
        echo_str = request.GET.get('echostr', '')

        try:
            check_signature(TOKEN, signature, timestamp, nonce)
        except InvalidSignatureException:
            return HttpResponse(status=403)

        msg = parse_message(request.body)
        if msg.type == 'event':
            if msg.event == 'subscribe' or msg.event == 'subscribe_scan':
                # 订阅时的事件
                reply = create_reply(u'菜鸟，来一局...', msg)
                return HttpResponse(reply.render())

        reply = TextReply(content=u'你好，有任何问题请直接回复，我们会尽快处理。', message=msg)
        return HttpResponse(reply.render())
``` 
###启用服务器配置(测试坏境)
* 登录[微信sanbox](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login), 扫描二维码并登陆。
* **修改接口配置信息**如图。在[urls.py]()增加
```
url(r'^wechat_echo$', csrf_exempt(views.WechatEcho.as_view()), name="wechat_echo")
```
![api](/images/wechat_api_url.jpeg)

###使用OAUTH方式获取微信用户授权。
* 登录[微信sanbox](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login), 扫描二维码并登陆。在[urls.py]()下增加一条url设置
```
url(r'^wechat/oauth2$', views.wechat_oauth2, name="wechat_oauth2")
```
根据下图修改**OAuth网页端授权页面**:
    ![api](/images/wechat_oauth1.png)  
    ![api](/images/wechat_oauth2.png)
* 依照微信文档[网页授权获取用户基本信息](http://mp.weixin.qq.com/wiki/17/c0f37d5704f0b64713d5d2c37b468d75.html),编写**用户同意授权**代码[BaseWeixinView](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/views.py)
* **拉取用户信息**[wechat_oauth2](https://github.com/smartfoosball/fooscloud/blob/dev/smartfoosball/views.py)部份代碼如下：

```
class BaseWeixinView(View):
    def dispatch(self, *args, **kwargs):
        if not self.request.user.is_authenticated():
            redirect_uri = urllib.urlencode({
                    'redirect_uri':
                        'http://' + self.request.get_host() + reverse("wechat_oauth2")})
            return redirect('https://open.weixin.qq.com/connect/oauth2/authorize?appid=%s&%s&response_type=code&scope=snsapi_userinfo&state=STATE#wechat_redirect' % (WX_APPID, redirect_uri))
        return super(BaseWeixinView, self).dispatch(*args, **kwargs)
    
def wechat_oauth2(request):
    code = request.GET.get('code')
    if code:
        params={'appid': WX_APPID,
                'secret': WX_SECRET,
                'code': code,
                'grant_type': 'authorization_code'}
        try:
            resp = requests.get('https://api.weixin.qq.com/sns/oauth2/access_token',
                                params=params)
            tokens = json.loads(resp.content)
            openid = tokens['openid']
            params = {'access_token': tokens['access_token'],
                      'openid': openid,
                      'lang': 'zh_CN'}
            resp = requests.get('https://api.weixin.qq.com/sns/userinfo', params=params)
            user = json.loads(resp.content)
```
2014-12-18