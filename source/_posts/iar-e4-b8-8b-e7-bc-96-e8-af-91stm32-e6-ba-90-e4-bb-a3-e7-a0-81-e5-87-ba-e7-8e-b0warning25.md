---
title: 'IAR下编译STM32源代码出现Warning[25]'
tags:
  - Cortex-M3
  - IAR
  - STM
  - STM32
  - 'Warning[25]'
  - 库函数
  - 编译
  - 警告
url: 812.html
id: 812
comments: false
categories:
  - STM32
  - 单片机
  - 嵌入式
  - 开发环境
date: 2016-05-08 17:21:56
---

    出现如下错误：Warning\[25\]: Label 'xxx' is defined pubweak in a section implicitly declared root

    是因为IAR在早期的版本里面使用了core_cm3文件，而在6以后高版本IAR中就不需要了。**IAR官方**也给出了解决方案：

* * *

    Warning\[25\]: Label 'xxxxx' is defined pubweak in a section implicitly declared root
=========================================================================================

EW targets:

ARM, STM8

EW component:

Assembler

Keywords:

assembly

Last update:

January 12, 2015

**Problem** After upgrading to... EWARM 7.10.1 EWSTM8 2.10.1 ...the Warning\[25\] is issued during assembly of a file that assembled without warning on earlier version of the Embedded Workbench.

**Solution** To avoid the warning, add **":NOROOT"** to the **"SECTION"** control directive. Add the **":NOROOT"** to the left of the ()-part of the line.

      PUBWEAK NMI_Handler
      SECTION .text:CODE:REORDER:NOROOT(1)
  NMI_Handler

**Background** The assembler is issuing Warning\[25\] for a deprecated assembler construction.

The deprecated assembler source construction looks like this:

      PUBWEAK NMI_Handler
      SECTION .text:CODE:REORDER(1)
  NMI_Handler

**Details** The assembler control directive of _"SECTION"_ consists of:

SECTION section :type \[:flag\] \[(align)\]

The change is **only** to be made among the **flag** items. I.e. don't change the**"SECTION" , "section" , ":type"** nor the **"\[(align)\]"** parts of the line. (For example if the _alignment_ is expressed as (2) then keep it at (2). (The (2) stands for an alignment of 4 bytes, as the (2) is the power of two to which the address should be aligned.))

The **"\[:flag\]"-part** can have these **flags:** ROOT (the default mode) or NOROOT and REORDER or NOREORDER (the default mode) Where now the Warning from the Assembler shows that the **"explicit noroot",** due to the directive **"PUBWEAK",** mismatch the default mode, which gives an **"implied root"** So the **"explicit noroot",** from **"PUBWEAK",** should be matched with the flag**"NOROOT".** The details for the assembler control directive of **"SECTION"** can be found in the chapter **"Section control directives"** in the **"IAR Assembler™ Reference Guide."** _All product names are trademarks or registered trademarks of their respective owners._  

* * *

#### **操作方法：**

        在启动文件里面startup\_stm32f10x\_xd.s（双击警告可以直接打开），在SECTION .text:CODE:REORDER(1)后面添加一个NOROOT，改成下面这个样子，

Reset_Handler  
LDR     R0, =SystemInit  
BLX     R0  
LDR     R0, =\_\_iar\_program_start  
BX      R0  
          
PUBWEAK NMI_Handler  
SECTION .text:CODE:REORDER:NOROOT(1)  

注意那个数字是在NOROOT后面的。每一个SECTION都添加后保存，再次编译警告消除。

* * *