---
title: 通过Python脚本标定ROS机器人的线速度和角速度
url: 1764.html
id: 1764
categories:
  - 建站
tags:
---

#### 开发环境：**Firefly-RK3399** \+ **Ubuntu 16.04** \+ **ROS Kinetic** \+ **Kinect V1 + STM32F103**

ROS By Example一书中讲到了rbx1_nav功能包中关于线速度和角速度的标定，但是由于代码当时运行的ROS版本较为古老，出现很多莫名其妙的问题。

kdl错误要改

cfg要改

transform_utils要移动到制定文件夹

http://www.ncnynl.com/archives/201701/1217.html

三个PY程序