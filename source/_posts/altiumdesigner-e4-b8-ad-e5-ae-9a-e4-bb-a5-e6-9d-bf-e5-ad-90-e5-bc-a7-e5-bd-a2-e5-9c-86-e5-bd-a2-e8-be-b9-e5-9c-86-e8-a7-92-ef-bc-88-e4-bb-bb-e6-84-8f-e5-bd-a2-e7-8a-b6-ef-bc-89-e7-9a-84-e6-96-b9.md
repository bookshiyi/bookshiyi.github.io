---
title: AltiumDesigner中定以板子弧形/圆形边/圆角（任意形状）的方法
tags:
  - AD
  - AltiumDesigner
  - DXP
  - PCB
  - 圆角
  - 弧形
  - 板子形状
url: 1201.html
id: 1201
comments: false
categories:
  - 电子工程
  - 电子设计自动化
  - 硬件设计
date: 2016-09-28 18:00:55
---

*   #### 0x00、▼以画板子弧形边为例，首先选择画弧工具Arc
    

#### ![arc](http://oarap.org/wp-content/uploads/2016/09/arc.png)

*   #### 0x01、▼在Keep Out Layer画出板子的外形
    

#### ![board_shape](http://oarap.org/wp-content/uploads/2016/09/board_shape.png)

*   #### 0x02、▼在Keep Out Layer中的线上右键-**Find Similar Object**，旨在选中在Keep Out Layer中表示板子外形的所有线条
    

#### ![find_similar_objects](http://oarap.org/wp-content/uploads/2016/09/find_similar_objects)

*   #### 0x03、▼让系统根据所选的对象确定板子形状
    

#### ![redefine_board_shape](http://oarap.org/wp-content/uploads/2016/09/redefine_board_shape.png)

*   #### 0x04、▼效果如下
    

#### ![](http://oss.bookshiyi.com/photo/2016/09/board_circle_3d_view.png)

     

####         这种方法可以推广到定义任意板子形状，只要在Keep Out Layer中用线条描述出预期的外形，一定要注意所选线段应为闭合曲线，在选中这些线条后让系统根据所选的线条定义板子形状即可。

 

* * *