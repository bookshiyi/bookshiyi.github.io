---
title: 微信公众平台客服桌面提醒脚本
tags:
  - js
  - 微信
url: 2639.html
id: 2639
categories:
  - 互联网
date: 2018-08-18 10:52:05
---

![](http://oss.bookshiyi.com/photo/2018/08/mpkf_weixin_notification_1.png-large)

![](http://oss.bookshiyi.com/photo/2018/08/mpkf_weixin_notification_2.png-large)

       微信公众平台的客服网页版如图所示，平台的客服人员如果想及时收到客户消息，要么一直盯着网页，要么接入一些流氓第三方平台。微信居然不能考虑做一个桌面提醒的功能这让人很难理解，只能自己动手丰衣足食了。

        不废话，先上代码：

使用方法：

        在chrome或firefox浏览器的应用商店中安装tampermonkey油猴脚本小插件

![](http://oss.bookshiyi.com/photo/2018/08/tampermonkey_chrome_1.png)

油猴大概长这样

        点击“添加新脚本”，导入我们的脚本代码

![](http://oss.bookshiyi.com/photo/2018/08/tampermonkey_chrome_2.png-large)

插件根据关键字自动识别脚本适配的网页

![](http://oss.bookshiyi.com/photo/2018/08/tampermonkey_chrome_3.png)

管理已安装脚本

        在“已安装脚本中”可以看到脚本的状态及设置

![](http://oss.bookshiyi.com/photo/2018/08/mpkf_weixin_notification_3.png)

申请桌面通知权限

        首次使用会申请桌面通知的权限，点击允许，至此完成了微信客服网页提醒的插件设置。

        之后如果有新的客户待接入或者客户发送的新消息会自动在桌面右下角弹出消息框，消息框长这样：

![](http://oss.bookshiyi.com/photo/2018/08/mpkf_weixin_notification_4.png)

桌面提醒消息

        然后就可以把客服页面最小化后台甚至切换到另一个虚拟桌面也不错过任何客服消息啦

        感谢同事**小明同学**提供的技术支持，目前的使用体验还不够好，未来还会继续升级。

        目前已经开源到[github](https://github.com/bookshiyi/https://github.com/bookshiyi/mpkf_weixin_notificationn)，有新想法的朋友可以提交更新，让小插件变得更好用。