---
title: 在ROS下使用USB_CAM驱动网络摄像头
tags:
  - cheese
  - ROS
  - usb_cam
  - v4l
url: 1825.html
id: 1825
comments: false
categories:
  - ROS机器人操作系统
  - 只文本模式
  - 开源软件
  - 机器人
  - 计算机视觉
date: 2017-04-19 11:13:45
---

#### 开发环境：**Firefly-RK3399** \+ **Ubuntu 16.04** \+ **ROS Kinetic** \+ **金贵S9**

        0x00.首先在插入USB摄像头后运行**lsusb**，应该能看到和下图红色框选部分类似的一个设备：

![](http://oarap.org/wp-content/uploads/2017/04/usb_cam_lsusb.png)

        0x01.运行**demsg**和**ls /dev/video***，应该能看到类似下图红色框选部分的文字：

![](http://oarap.org/wp-content/uploads/2017/04/demsg_ls_dev_video.png)

** 重点**是/dev下一定要有Video*，如果你的USB摄像头没有对应的Video*（一般来说笔记本自带的摄像头是video0，在笔记本电脑外接usb摄像头应该会有video0和video1），那么很可能你的USB摄像头驱动并没有被Linux支持，需要解决linux下摄像头的驱动问题（本文不展开讨论）。

        0x02.安装**cheese**（作为监视窗口）：

 如果在你的Teminal中输入并运行cheese如果提示未安装，你可以运行一下命令安装：

sudo apt-get install cheese

 安装完毕后输入并运行**cheese**，应该能看到类似下图的画面**：**

![](http://oarap.org/wp-content/uploads/2017/04/usb_cam_cheese.png)

 可以看到cheese提供了一些关于摄像头的参数调整，到了这一步可以证明你的摄像头能够完整的被Linux驱动起来。

        0x03.从git下载**usb_cam**源码并编译：

cd catkin_wsgit 
clone https://github.com/bosh-ros-pkg/usb_cam.git
catkin_make

        0x04.安装**v4l-utils**（Video4Linux）：

sudo apt-get install v4l-utils

0x05.参考usbcam-test.launch写一个启动文件，更改参数：

   

 参数解释：

** image\_width、image\_height**：分辨率选项，请根据你的摄像头支持（cheese中可以看到）和计算机性能合理调整大小；

 **pixel_format** (string, default: "mjpeg") Possible values are **mjpeg**, **yuyv**, **uyvy**，如果你在rviz可视化中出现下图情况请尝试更改该参数**：**

![](http://oarap.org/wp-content/uploads/2017/04/usb_cam_launch_no_mjpeg.png) ![](http://oarap.org/wp-content/uploads/2017/04/usb_cam_launch_r_g.png)

        0x05.启动usb_cam.launch、启动rviz可视化、运行rostopic list：

![](http://oarap.org/wp-content/uploads/2017/04/usb_cam_rviz_rostopic.png)

 至此，你的USB摄像头已经可以完美的和ROS系统进行通信。

uvc_cam

* * *

 笔者使用的摄像头如下（感谢室友**滕先生**提供资源支持）：

![](http://oarap.org/wp-content/uploads/2017/04/jingui_s9_usb_cam.png)

* * *

        最后感谢FireFly团队提供的**RK3399**高性能、奢侈配置的开发板(点击图片了解详情)：

[![](http://oarap.org/wp-content/uploads/2017/04/firefly_rk3399_preview.png)](http://www.t-firefly.com/zh/firenow/Firefly-rk3399/)

* * *

 参考：

 《ROS Robotics Projects》

 http://www.cnblogs.com/CZM-/p/6024600.html

 http://www.cnblogs.com/qixianyu/p/6575276.html