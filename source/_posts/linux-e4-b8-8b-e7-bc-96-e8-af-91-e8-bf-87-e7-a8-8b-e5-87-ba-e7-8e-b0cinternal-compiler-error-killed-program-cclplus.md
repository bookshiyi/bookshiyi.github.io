---
title: 'Linux下编译过程出现c++:internal compiler error: Killed (program cclplus)'
tags:
  - cmake
  - linux
  - ROS
  - swap
  - Ubuntu
url: 1642.html
id: 1642
comments: false
categories:
  - Linux
  - ROS机器人操作系统
  - 开源
  - 开源软件
  - 软件设计
date: 2017-04-06 09:52:24
---

0x00 问题描述：

使用Cmake在Ubuntu上编译ROS功能包时出现如下错误：

c++: internal compiler error: Killed (program cclplus)
Please submit a full bug report,

0x01 原因分析：

大概是因为内存不足（通过进程查看器可以看到编译过程中内存使用率一直接近100%），内核认为编译进程长时间占用内存所以将其结束；

0x02 解决方案：

使用临时使用交换分区，运行以下命令：

sudo dd if=/dev/zero of=/swapfile bs=64M count=16
sudo mkswap /swapfile
sudo swapon /swapfile