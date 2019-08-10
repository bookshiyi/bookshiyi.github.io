---
title: robot_pose_ekf
url: 1755.html
id: 1755
categories:
  - 建站
tags:
---

robot\_pose\_ekf 订阅哪些话题，发布TF http://blog.csdn.net/eaibot/article/details/51405152   robot\_pose\_ekf发布了odom话题，但是消息类型却是geomtry\_msgs/，导航包订阅的是nav\_msgs/odometry 所以导致tf和odom显示不对应