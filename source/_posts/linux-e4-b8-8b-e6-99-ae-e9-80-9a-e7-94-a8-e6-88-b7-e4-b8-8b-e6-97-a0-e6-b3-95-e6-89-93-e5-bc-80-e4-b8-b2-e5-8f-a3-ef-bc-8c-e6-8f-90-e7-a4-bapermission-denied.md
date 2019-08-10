---
title: Linux下普通用户下无法打开串口，提示Permission denied
tags:
  - linux
  - ROS
  - ttyUSB
  - usb
  - 串口
  - 权限
url: 1752.html
id: 1752
comments: false
categories:
  - Linux
  - ROS机器人操作系统
  - 开源软件
date: 2017-04-12 20:34:30
---

在学习ROS的过程中我们不可避免的要和串口打交道，可能是硬件的USB-TTL、USB-RS232、USB-TTL、USB蓝牙、板载蓝牙或者是软件的虚拟串口等等。

可以通过图形化串口调试工具**cutecom**等打开串口并通信，但是在运行某些ROS节点的时候需要打开串口时，却提示：

Could not open serial port '/dev/ttyUSB0'（ttyUSB*、rfcomm*、ttyACM*等）

Permission denied

含义为当前用户缺少该文件的读写权限

于是呆萌的我开始各种试错：

1.  尝试运行**sudo rosrun base\_controller base\_controller**，结果ros开头的命令并不支持sudo操作；
2.  尝试运行**sudo chmod 666 /dev/ttyUSB0，**这样可以临时解决，但每次重新插拔或重启都要运行这个命令；
3.  一怒之下重装系统，把ROS安装在root目录下，然后每次都登入root用户，麻麻再也不用担心任何权限的问题啦，感觉寄几是最棒的（尽管可行，但是非常不推荐用root账户操作文件，因为这可能会伤害你的计算机）。

* * *

##### **解决方案**：

在 **/etc/udev/rules.d** 目录下面添加一个 **20-usb-serial.rules**文件，内容如下：

1.  KERNEL=="ttyUSB*"  MODE="0666"
2.  KERNEL=="rfcomm*"  MODE="0666"
3.  KERNEL=="ttyACM*"  MODE="0666"

 

参考资料：http://blog.csdn.net/vikingmei/article/details/8242836

 

* * *