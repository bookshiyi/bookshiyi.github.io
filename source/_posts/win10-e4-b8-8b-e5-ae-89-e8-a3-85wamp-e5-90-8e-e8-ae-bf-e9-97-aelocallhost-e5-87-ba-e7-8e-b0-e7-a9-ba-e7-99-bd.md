---
title: WIN10下安装WAMP后访问locallhost出现空白
tags:
  - 80端口
  - apache
  - locallhost
  - wamp
  - win10
url: 823.html
id: 823
comments: false
categories:
  - 建站
date: 2016-05-18 18:13:06
---

        2015年7月28日，微软宣布低版本的windows用户一年内可以免费升级到Windows10，言外之意过了一年可就不一定啦 ，机智的博主不会放过这次机会，在还有不到100天的时间就到了微软履行承诺的时候笔者更新了Windows10操作系统，突然发现WAMP Server不好用了，访问locallhost出现的也是一片空白，仔细看wamp的图标成了橘黄色->![wam_unusable](http://oarap.org/wp-content/uploads/2016/05/wam_unusable.jpg)，如果你也出现了类似的问题请按照如下的步骤进行排查。

> ##### **左键WAMP的图标->Apache->Service->测试80端口**
> 
> ![test_port80](http://oarap.org/wp-content/uploads/2016/05/test_port80.png) **如果显示** **“Yout port 80 is actually used by ：** **Server：Microsoft-IIS/10.0”，** ![IIS_port80](http://oarap.org/wp-content/uploads/2016/05/IIS_port80.png) **        说明IIS服务占用了80端口，由于笔者不经常使用IIS服务，所以就在任务管理器里面直接结束了有关IIS的服务进程，** ![task_ management_iis](http://oarap.org/wp-content/uploads/2016/05/task_-management_iis.jpg)

   重启WAMP程序，哈哈，图表变成了绿色，网页也出来了，又可以快乐的码代码了。    

>         **不过好景不长，重启过后又不能访问了，总这么手动的结束进程可不是什么好办法，于是经过一番研究，在“计算机->管理”里面发现“World Wide Web Publishing Service”这个服务居然是自动启动的状态，**
> 
> ![computer_managment](http://oarap.org/wp-content/uploads/2016/05/computer_managment.jpg)
> 
> **        直接禁止启动，**
> 
> ![forbid_startup](http://oarap.org/wp-content/uploads/2016/05/forbid_startup.jpg)

        这样再也不怕重启过后IIS占用80端口了。

* * *

        可是需要同时使用IIS和WAMP的同学表示不服了，禁掉了IIS的话还怎么码代码，于是就有了第二种解决办法（修改WAMP不使用默认的80端口），这种办法可以实现IIS和WAMP并存。

> **        右键WAMP->Apache->httpd.conf，如下图**
> 
> **![httpd_conf](http://oarap.org/wp-content/uploads/2016/05/httpd_conf.png)**
> 
> **        搜索“Listen 80”和“ServerName localhost:80”**
> 
> **![listen80](http://oarap.org/wp-content/uploads/2016/05/listen80.png)![servername_locallhost_80](http://oarap.org/wp-content/uploads/2016/05/servername_locallhost_80.png)**
> 
> **        直接修改为你喜欢的端口，然后不要忘记保存。不过不要高兴得太早，还没完成，在wamp安装目录下的wampmanager.tpl文件，记事本打开：**
> 
> **![locallhost](http://oarap.org/wp-content/uploads/2016/05/locallhost.jpg)**
> 
> **        在localhost后面添加8088端口，保存，退出并重新打开wamp生效。（其实，wampmanager.ini文件中的类似的URL地址也随之更改了）**

 

 这下就彻底解决了80端口的占用问题。

 

* * *