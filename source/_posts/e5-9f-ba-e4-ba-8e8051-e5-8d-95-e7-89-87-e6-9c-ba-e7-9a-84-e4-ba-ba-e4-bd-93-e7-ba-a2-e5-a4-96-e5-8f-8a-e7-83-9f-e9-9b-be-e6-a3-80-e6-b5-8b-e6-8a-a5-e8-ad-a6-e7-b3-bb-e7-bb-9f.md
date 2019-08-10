---
title: 基于8051单片机的人体红外及烟雾检测报警系统
tags:
  - 89c51
  - 人体红外
  - 可燃气体
url: 225.html
id: 225
comments: false
categories:
  - MSC-8051
  - 单片机
date: 2014-03-01 20:16:22
---

        由于比较匆忙，只剩下几张照片和源代码（其实是实在没什么可以说的，功能太简单了）。

        这个是我自学单片机的第一个大作业，也是走进电子世界大门的第一步，虽然它功能不多，系统简单，却是我初心的起点。   ![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_1.jpg-w800_wm)![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_2.jpg-w800_wm)

![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_3.jpg-w800_wm)

![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_4.jpg-w800_wm)

![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_5.jpg-w800_wm)

![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_6.jpg-w800_wm)![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_7.jpg-w800_wm)![](https://bookshiyi.oss-cn-qingdao.aliyuncs.com/photo/2014/03/89c51_MQ2_ir_buzz_7.jpg-w800_wm)

 

        本来是计划做一个移动气象监测车，由于关键的无线传输部分（NRF24L01）的通信协议没有调通，又到了比赛提交作品的deadline，所以只能放弃监测车，改为人体红外和可燃气体检测报警系统，其实说来比较简单：系统USB母口为+5V输入，旁边的插针支持+5V~+8V供电输入（使用LM7805稳压），两个传感器：可燃气体传感器（MQ-2）人体红外传感器都是数字量输入，当检测到有可燃气体时系统发出声光报警（红色LED闪烁，蜂鸣器鸣叫），当检测到人体红外时系统发出声光报警（蓝色LED闪烁，蜂鸣器鸣叫）。

        后来才发现，那么简单的功能用单片机去做简直是极大的浪费，完全可以使用几个三极管或这门电路实现上述功能，不仅简化了软硬件的设计，更减低了系统功耗和开发成本。

* * *