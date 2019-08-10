---
title: 国外VPS搭建PAC代理服务器
tags:
  - pac
  - vps
  - 代理服务器
url: 568.html
id: 568
comments: false
categories:
  - 信息安全
  - 信息技术
  - 建站
date: 2016-03-18 20:00:43
---

郑重声明
====

*   #### 文章内容仅供**研究**、**学习**参考使用，请自觉遵守当地法规浏览互联网站点，用于非法领域者自行承担一切法律后果。
    

*   在中国这片神奇的大地上，一些国外的网站我们是无法直接访问的，于是技术宅们开始搭建梯子绕过IP封锁、端口封锁、内容过滤、域名劫持这些墙，也衍生出了许多不同的方案。

### 主流方案比较：

> ##### **Shadow*socks**
> 
> 非常流行的方案，在2015年的时候作者被迫在github上面删除了源码。
> 
> ##### **V\*P\*N: PPTP、L2TP、IPSEC、Open\*VP\*N**
> 
> 与服务器简历加密连接，pptp基本被封杀；l2tp/ipsec基本可以使用；最后的方案搭建难度较大，但是被屏蔽的可能性小，安全系数极高，缺点是默认不能自动分流。
> 
> ##### **PAC代理**
> 
> 搭建快速，智能分流模式，不易屏蔽。缺点是不具有太强的加密措施。

   

* * *

 

### 1.服务器的购买

本文的服务器是从CosmosTeck上面购买的，OpenVZ架构，内存128MB，硬盘2GB，150GB每月，年付40RMB。

> 官网链接：[https://www.cosmosteck.com/](https://www.cosmosteck.com/) 我的推广：[https://www.cosmosteck.com/clients/aff.php?aff=079](https://www.cosmosteck.com/clients/aff.php?aff=079)

如果不喜欢推广链接的形式可以访问官网的地址。

### 2.PAC搭建

本文介绍的pac服务器是基于openvz架构和centos6_86系统搭建的，其他平台尚未测试。

*   修改vps系统时间为上海时区

rm -rf /etc/localtime
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
date

*   运行以下代码

`setenforce 0 ulimit -n 800000 echo "* soft nofile 800000" >> /etc/security/limits.conf echo "* hard nofile 800000" >> /etc/security/limits.conf echo "alias net-pf-10 off" >> /etc/modprobe.d/dist.conf echo "alias ipv6 off" >> /etc/modprobe.d/dist.conf killall sendmail /etc/init.d/postfix stop chkconfig --level 2345 postfix off chkconfig --level 2345 sendmail off yum -y install squid wget wget http://github.itzmx.com/1265578519/PAC/master/squid/centos-squid.conf -O /etc/squid/squid.conf mkdir -p /var/cache/squid chmod -R 777 /var/cache/squid squid -z service squid restart chkconfig --level 2345 squid on iptables -t nat -F iptables -t nat -X iptables -t nat -P PREROUTING ACCEPT iptables -t nat -P POSTROUTING ACCEPT iptables -t nat -P OUTPUT ACCEPT iptables -t mangle -F iptables -t mangle -X iptables -t mangle -P PREROUTING ACCEPT iptables -t mangle -P INPUT ACCEPT iptables -t mangle -P FORWARD ACCEPT iptables -t mangle -P OUTPUT ACCEPT iptables -t mangle -P POSTROUTING ACCEPT iptables -F iptables -X iptables -P FORWARD ACCEPT iptables -P INPUT ACCEPT iptables -P OUTPUT ACCEPT iptables -t raw -F iptables -t raw -X iptables -t raw -P PREROUTING ACCEPT iptables -t raw -P OUTPUT ACCEPT service iptables save`

### 3.添加PAC文件

*   将pac文件放置在服务器的/var/www/html文件夹内

pac文件下载[oarap.pac](http://oarap.org/wp-content/uploads/2016/03/oarap.pac_.rar)

### 4.禁用ipv6

*   首先在/etc/modprobe.d/dist.conf结尾添加

`echo "alias net-pf-10 off" >> /etc/modprobe.d/dist.conf echo "alias ipv6 off" >> /etc/modprobe.d/dist.conf`

*   运行下列命令后重启

`echo "net.ipv6.conf.all.disable_ipv6 =1" >> /etc/sysctl.conf echo "net.ipv6.conf.default.disable_ipv6 =1" >> /etc/sysctl.conf sysctl -p`

### 4.常见问题

Q：kvm和xen架构或centos5/7可以使用么？

*   A：笔者没有对其他平台进行测试，无法保证教程的有效性。

Q：设置完后无法上网是什么原因

*   A：请在浏览器输入你的IP地址或者域名，若没有发现PAC文件，请检查PAC文件的路径

通过Putty等程序连接到服务器，看是server否能ping通网络。  

### **敬告**

* * *

        Wall存在的意义是维护民族团结，切莫因掌握一点技术而沾沾自喜，是因为你的一举一动都在运营商的监控中，请仔细思考：“Wall不仅仅是对有害信息的隔离、屏蔽，更是一个优秀的筛选器”，所以请诸位心存善意，勿念侥幸。