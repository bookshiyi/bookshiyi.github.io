---
title: ROS系统中.launch文件中实现if逻辑判断
tags:
  - launch
  - ROS
  - Ubuntu
  - xml
url: 1785.html
id: 1785
comments: false
categories:
  - Linux
  - ROS机器人操作系统
  - 机器人
  - 软件设计
date: 2017-04-13 11:16:45
---

.launch文件是ROS中一种描述多节点启动的XML类文件

XML语言是一种描述类的脚本语言，在ROSLaunch中可以采用如下方式实现逻辑判断：

* * *

<arg name="driver_enable" default="true"/>

<group if="$(arg driver_enable)">

<include file="$(find openni2_launch)/launch/openni2.launch"/>

</group>

使用如下命令调入参数：

roslaunch \[pkg\] \[node\] driver_enable:=false

* * *

参考：

http://blog.csdn.net/zqxf123456789/article/details/52497833

http://wiki.ros.org/roslaunch/XML