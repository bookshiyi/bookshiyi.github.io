---
title: 搬瓦工(BandWaGonHost)快速搭建openvpn和ss
tags:
  - openvpn
  - ss
  - 搬瓦工
  - 梯子
  - 科学上网
url: 1360.html
id: 1360
comments: false
categories:
  - 互联网
  - 信息安全
  - 信息技术
  - 建站
  - 软件设计
  - 静思
date: 2016-11-13 13:01:56
---

郑重声明
====

*   #### 文章内容仅供**研究**、**学习**参考使用，请自觉遵守当地法规浏览互联网站点，用于非法领域者自行承担一切法律后果。
    

 

### **简介**

* * *

        BandWaGonHost的特点：OpenVZ架构、一键部署OpenVPN和SS、任意切换IP地址和数据中心、无条件退单、支持PayPal、UnionPay（银联）、AliPay（支付宝）

        搬瓦工官网主域名：http://BandWaGonHost.com，但服务器不稳定，可能无法访问。官方备用的镜像域名：http://bwh1.net。

        在网上注册的时候仔细甄别域名，以防进入不法分子的钓鱼网站。(下图是某流氓网站的做法)

![](http://oss.bookshiyi.com/photo/2016/11/fake_bandwagong.jpg)

### **教程**

* * *

*   ### 注册：
    
*   通过该链接注册将给我带来一点收入，也会给你优惠 ： [https://bwh1.net/aff.php?aff=11543](https://bwh1.net/aff.php?aff=11543)
*   如果介意，可点击纯净链接：[https://bwh1.net](https://bwh1.net)

  下单的时候添写邀请码：IAMSMART5K717Q，会为你优惠4%左右。

*   下单(优惠)和支付的过程如下（支持Alipay）；

![](http://oarap.org/wp-content/uploads/2016/11/bwh1_validate_code.png) 账单产生的优惠类似这样 ![](http://oarap.org/wp-content/uploads/2016/11/bwh1_cart.png)

*   支付成功后可以从Services-MyServices中能找到已经购买的服务器，通过KiwiVM控制面板管理服务器；

![bwh_ovpn_ss_1](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_1.jpg)

*   首次使用需要在关闭服务器后安装CentOS系统；

![bwh_ovpn_ss_2](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_2.png)

![bwh_ovpn_ss_3](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_3.jpg)

*   OpenVPNServer面板中一键安装OpenVPN；

![bwh_ovpn_ss_4](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_4.png)

*   接下来会调用搬瓦工官网的一键安装脚本；

![bwh_ovpn_ss_5](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_5.png)

*   安装好后就可以下载Key文件和客户端；![bwh_ovpn_ss_6](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_6.png)

*   在ShadowServer面板中一键安装SS；

![bwh_ovpn_ss_7](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_7-1.png)

![bwh_ovpn_ss_8](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_8.png)

*   安装完成后会自动生成参数；

![bwh_ovpn_ss_9](http://oarap.org/wp-content/uploads/2016/11/bwh_ovpn_ss_9.png)

        客户端的连接方法不再赘述。

### **敬告**

* * *

        Wall存在的意义是维护民族团结，切莫因掌握一点技术而沾沾自喜，是因为你的一举一动都在运营商的监控中，请仔细思考：“Wall不仅仅是对有害信息的隔离、屏蔽，更是一个优秀的筛选器”，所以请诸位心存善意，勿念侥幸。