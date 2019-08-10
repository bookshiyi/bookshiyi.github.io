---
title: 国外VPS使用NET-SPEEDER提高连接速度、降低丢包率
tags:
  - net-speeder
  - pac
  - ping
  - vps
  - 丢包
  - 加速
  - 科学上网
url: 881.html
id: 881
comments: false
categories:
  - 信息安全
  - 建站
date: 2016-05-23 21:42:26
---

        之前使用国外VPS搭建了PAC代理服务器，在使用铁通网络的时候ping=200ms，丢包率不高，后发现移动宽带对Phoenix, AZ,的VPS线路并不友好，下载时候网速仅20+KB/s，看到一些网友提到了使用net-speeder加速VPS的连接速度，于是便实践了一番。

        当我们使用自己的设备连接国外VPS的时候，信号要穿越半个地球然后原路返回才完成一次握手，在复杂的网络环境中，如果等待延时过长这个数据帧就会直接被销毁在中途的路由设备，导致了丢包（使用ping命令是没有丢包重传机制的）的情况。为了解决丢包问题，最简单粗暴的方法就是双倍发送，即同一份数据包发送两份。这样的话在服务器带宽充足情况下，丢包率会平方级降低。直接优点是降低丢包率，直接缺点是耗费双倍流量。一些延伸影响是更容易触发快速恢复逻辑，避免了丢包时窗口缩减过快，一定程度也能提高网络速度。

        NET-SPEEDER：**在高延迟不稳定链路上优化单线程下载速度** ，项目Githu主页：[https://github.com/snooda/net-speeder](https://github.com/snooda/net-speeder) ，在此感谢[snooda](http://www.snooda.com/)的无私奉献。

       博主VPS配置：VPS - OVZ-128MB，Centos-6-x86。

#### **安装：**

> 1：下载源码并解压
> 
> wget https://github.com/snooda/net-speeder/archive/master.zip
> unzip master.zip
> 
> 2：准备编译环境   2.1 debian/ubuntu： #安装libnet-dev：
> 
> apt-get install libnet1-dev
> 
> #安装libpcap-dev：
> 
> apt-get install libpcap0.8-dev
> 
>   2.2 centos： #下载epel：https://fedoraproject.org/wiki/EPEL/zh-cn 例：CentOS6 64位：
> 
> wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
> 
> #（如果是centos5，则在epel/5/下） #安装epel：
> 
> rpm -ivh epel-release-6-8.noarch.rpm
> 
> #然后即可使用yum安装：
> 
> yum install libnet libpcap libnet-devel libpcap-devel
> 
>    

#### **编译：**

> #Linux Cooked interface使用编译（venetX，OpenVZ）：
> 
> sh build.sh -DCOOKED
> 
> #普通网卡使用编译（Xen，KVM，物理机）：
> 
> sh build.sh
> 
>  

#### **启动：**

> 1.手动启动 #参数：./net_speeder 网卡名 加速规则（bpf规则） #例：OVZ架构中的用法(加速所有ip协议数据)：
> 
> ./net_speeder venet0 "ip"
> 
> 或者使用（在执行之前请将net_speeder这个文件移动到/usr/bin文件夹中） `nohup /usr/bin/net_speeder venet0 "ip" >/dev/null 2>&1 &` 2.自动启动 #将加速服务添加到开机启动项中（在执行之前请将net_speeder这个文件移动到/usr/bin文件夹中） `echo 'nohup /usr/bin/net_speeder venet0 "ip" >/dev/null 2>&1 &' >> /etc/rc.local`

 

#### **Q&A:**

* * *

 

##### 1.怎样确定我的服务器加速成功。

 

> 方法一：ssh客户端中输入下列命令
> 
> top
> 
> 应该会出现类似下图的情况 ![task_net_speeder](http://oarap.org/wp-content/uploads/2016/05/task_net_speeder.jpg)

 

> 方法二 使用非windows命令工具，ping 你的服务器会在返回的命令里出现（DUP!），如下图 ![](http://oarap.org/wp-content/uploads/2016/05/ping_value.jpg)

 

* * *

##### 2.**ping 服务器的时候会连续返回多个（DUP!）**

> 应该是重复开启了多个net-speeder服务，先结束掉所有的net-speeder服务
> 
> killall net_speeder
> 
> 然后重新运行net-speeder服务
> 
> `nohup nohup /usr/bin/net_speeder venet0 "ip" >/dev/null 2>&1 &` 如果使用**centos**请查看/etc/rc.d/rc.local中是否重复启动加速服务。 如果使用**ubuntu**请查看/etc/rc.local中是否重复启动加速服务。

##### 3.**使用加速服务器之后网速还是很慢**

> 可能是你的服务器所在线路特别拥堵、丢包严重造成的，建议尝试开启多个加速服务（一个数据包不止发两次，甚至三次四次，以此来降低丢包率），但是并不是一味发送的多就会带来速度上的提升（而且加速服务越多也会更多的浪费流量），所以请在开启不同服务个数的情况下测试连接速率。（博主的VPS使用两个加速服务时效果较好，正常来说最多开启四个就足矣了）

 

* * *