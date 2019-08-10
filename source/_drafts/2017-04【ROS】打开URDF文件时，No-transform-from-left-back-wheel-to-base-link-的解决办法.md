---
title: '2017-04【ROS】打开URDF文件时，No transform from [left_back_wheel] to [base_link]的解决办法'
url: 1632.html
id: 1632
categories:
  - 建站
tags:
---

check_urdf *.urdf   检查没有任何问题 [hitgavin](http://blog.csdn.net/hitgavin/article/details/51997379) 也有类似的问题，但我进行如下操作后

1.  sudo apt-get install unicode

发现问题并没有得到解决。   把continius修改为fixed可以 robot和link之间不能空行 ![](http://oarap.org/wp-content/uploads/2017/04/robot_model_urdf_bug.jpg)   参考： http://answers.ros.org/question/201372/rviz-keep-saying-no-transform-from-front\_left-to-base\_link/