---
title: STM32平台上使用PCA9685
tags:
  - PCA9685
  - PWM
  - STM32
  - 舵机
  - 驱动
url: 1068.html
id: 1068
comments: false
categories:
  - STM32
  - 单片机
  - 嵌入式
  - 电子工程
  - 硬件设计
  - 软件设计
date: 2016-09-29 10:16:23
---

        PCA9685是一款基于IIC总线通信的12位精度16通道PWM波输出的芯片，该芯片最初由NXP推出时主要面向LED开关调光，但就目前国内的形式来看，好像在被Arduino在舵机控制领域使用的更广泛。

        该模块由于主要活跃在Aruino周边，所以在使用Arduino开发其底层驱动库是十分完善的，但对于单片机开发人员就不太友好了，需要自行根据用户手册在单片机上编写底层的驱动。（[NXP官方PCA9685文档](http://www.nxp.com/zh-Hans/products/power-management/lighting-driver-and-controller-ics/i2c-led-display-control/16-channel-12-bit-pwm-fm-plus-ic-bus-led-controller:PCA9685?fpsp=1&tab=Documentation_Tab)）

PCA9865模块一般长这样

![pca9685_模块](http://oss.bookshiyi.com/photo/2016/09/pca9685_module.jpg)

PCA9685模块支持级联，也就是在IIC总线上挂载多个芯片（如下图）。

![pca9685_级联](http://oss.bookshiyi.com/photo/2016/09/pca9685_cascade.jpg)

其地址的分配是通过模块右上方的短接焊盘来确定的，从A0-A5表示地址的最低位到最高位，也就是最多可级联2^5=32个模块，默认从0X40开始，所以每个模块的地址表示为：A5\*32 + A4\*16 + A3\*8 + A2\*4 + A1\*2 + A0\*1 + 0X40

![PCA9685_地址分配](http://oss.bookshiyi.com/photo/2016/09/pca9685_address.jpg)

#### **[点我下载](http://oss.bookshiyi.com/file/2016/09/Pca9685_Driver.rar)**PCA9685在STM32平台上的驱动包

   

* * *