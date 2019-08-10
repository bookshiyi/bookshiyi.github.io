---
title: 'IAR[40701]错误解决方法：通过STVP修复STM8芯片损坏、修改/修复Optioin Byte'
tags:
  - IAR
  - OptionByte
  - STM8
  - STVP
  - 选项字节
url: 1187.html
id: 1187
comments: false
categories:
  - STM8
  - 单片机
  - 嵌入式
  - 开发环境
  - 电子工程
  - 硬件设计
date: 2016-09-29 08:42:46
---

        在使用IAR向STM8系列芯片烧写程序的时候可能出现如下错误：

> Connection error (usb://usb): gdi-error \[40701\]: option bytes read error: not complemented; please use a programmer

        经过查阅数据手册后得知：

![option_byte](http://oarap.org/wp-content/uploads/2016/09/option_byte.png)

![stm8_rop](http://oarap.org/wp-content/uploads/2016/09/stm8_ROP.png)

![](http://oss.bookshiyi.com/photo/2016/09/memory_read.png)

![option_byte_register](http://oarap.org/wp-content/uploads/2016/09/Option_Byte_Register.png)

* * *

#### 修复方法：

        STVP是意法半导体官方推出的芯片烧录软件，可以通过IAP和ICP的方式向PROGRAM MEMORY、DATA MEMORY和**OPTION BYTE**读写程序.

        当OptionByte出现错误的时候是无法通过宿主机IDE向Flash编程的，此时应该修复OptionByte（即向OptionByte编程）只能使用官方的STVP（ST Visual Programmer）烧写程序，需要对OptionByte重新烧写，然而需要打开ROP（即Read Out Protection）位并写入，尽管写入后的芯片的OptionByte已经修复正常，但是由于OptionByte中的ROP处于开启状态，此时的STM8中的FLASH区是无法通过IAR使用SWIM方式写入编写好的用户程序，所以此时应后关闭ROP位并下载，至此OptionByte的修复成功。

![stvp_option_byte](http://oarap.org/wp-content/uploads/2016/09/stvp_option_byte.png)

* * *