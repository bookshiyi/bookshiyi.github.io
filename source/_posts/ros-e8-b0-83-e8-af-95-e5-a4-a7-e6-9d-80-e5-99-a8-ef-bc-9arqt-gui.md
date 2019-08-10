---
title: ROS调试大杀器：rqt_gui
tags:
  - ROS
  - rqt
  - slam
  - Ubuntu
  - 机器人
  - 机器人操作系统
url: 1553.html
id: 1553
comments: false
categories:
  - ROS机器人操作系统
  - 信息技术
  - 开源
  - 开源软件
  - 机器人
  - 软件设计
date: 2017-03-28 17:00:01
---

        ROS提供了一套完整的图形化调试工具，可是在学习的过程中发现命令太多，很多需要用的时候却记不起还有这样的命令，而大多数的教科书/教程上都指出各种的rqt（Robot QT）的具体gui命令，却很少提到 **rosrun rqt\_gui rqt\_gui**这个图形化调试工具合集。

        确保你的节点管理器已经打开(roscore)，在新的Teminal中输入：

rosrun rqt\_gui rqt\_gui

![](http://oarap.org/wp-content/uploads/2017/03/rosrun__rqt_gui.jpg)

        ▲如图所示，默认是没有任何显示；

![](http://oarap.org/wp-content/uploads/2017/03/rqt_gui_visualization.jpg)

        ▲可以通过添加插件的方式打开你需要的gui调试器；

![](http://oarap.org/wp-content/uploads/2017/03/multi_rqt_gui.png)

        ▲而且还可以多个GUI调试界面存在同一个活动窗口下。

*    再也不用记复杂的rqt命令了，每次需要图形调试仅运行**rosrun rqt\_gui rqt\_gui**即可。

* * *