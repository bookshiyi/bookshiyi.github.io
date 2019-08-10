---
title: 多计算机间运行ROS实现分布式计算
tags:
  - ROS
  - 机器人
  - 节点
url: 1604.html
id: 1604
categories:
  - Linux
  - ROS机器人操作系统
  - 开源
  - 开源软件
  - 机器人
---

gedit /etc/hosts your\_ip   your\_hostname   主机端的.bashrc修改i如下（运行sudo gedit ~/.bashrc） export ROS\_MASTER\_URI=http://192.168.1.130:11311 export ROS\_IP=192.168.1.190（本机IP） 在主机上ssh <laptop\_user>@<laptop_ip>