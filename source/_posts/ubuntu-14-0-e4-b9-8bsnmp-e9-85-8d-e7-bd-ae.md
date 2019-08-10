---
title: Ubuntu 14.0 之SNMP配置
tags:
  - snmp
  - Ubuntu
  - 监控宝
url: 86.html
id: 86
comments: false
categories:
  - 建站
date: 2016-02-27 22:10:08
---

    对比阿里云和监控宝的服务器监控，阿里云的简单易上手，监控宝的强大人性化，故为服务器加装了监控宝，采用的内网采集器的形式，需要开启SNMP服务，在这个过程中却遇到了一些问题，旧版本的教程里所提到的com2sec根本没有在snmpd.conf里面出现。解决办法如下：

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-

1\. SNMP安装

运行如下两个命令

apt-get install snmp \[enter\]

apt-get install snmpd \[enter\]

顺利运行完毕，使用如下命令测试一下

lsof -i:161

如果输出了正在运行snmp协议，便说明安装OK。

2\. SNMP配置（重点）

我的SNMP配置文件/etc/snmp/**snmpd.conf**与网上早年的一些资料不同，主要是 压根没有出现com2sec。

-----------------------------------配置**snmpd.conf****\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-**

将下面这一行

agentAddress udp:127.0.0.1:161

注释掉，即

#agentAddress udp:127.0.0.1:161

然后将原来的这一行

#agentAddress udp:161,udp6:\[::1\]:161

去掉注释，即

agentAddress udp:161,udp6:\[::1\]:161

这样便可以实现snmp的远程监听了。

但修改后cacti服务器还是无法监测到CPU、内存、流量的数据，所以需要再做如下修改：

在snmpd.conf中找到下面的内容 view   systemonly  included   .1.3.6.1.2.1.1 view   systemonly  included   .1.3.6.1.2.1.25.1在下面加上一行 view   systemonly  included   .1   80 这样就允许监听所有设备了。

完成所有修改后，重启snmp

service snmpd restart

本地测试SNMP是否监测各类指标的方法：运行如下命令

snmpwalk -v 2c -c public localhost

如果输出结果有好多页，应该是设置成功了！