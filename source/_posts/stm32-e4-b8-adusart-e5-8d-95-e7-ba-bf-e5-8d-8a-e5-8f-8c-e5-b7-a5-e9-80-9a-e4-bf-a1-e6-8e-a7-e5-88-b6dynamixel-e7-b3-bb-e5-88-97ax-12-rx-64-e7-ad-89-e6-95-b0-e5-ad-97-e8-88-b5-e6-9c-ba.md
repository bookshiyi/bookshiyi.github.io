---
title: STM32中USART单线半双工通信/控制Dynamixel系列AX-12 RX-64等数字舵机
tags:
  - AX-12
  - Dynamixel
  - OD门
  - RX-64
  - STM32
  - UART
  - USART
  - 上拉电阻
  - 串口
  - 半双工
  - 单线半双工
  - 开漏输出
  - 推挽
  - 数字舵机
  - 线与
url: 1379.html
id: 1379
comments: false
categories:
  - STM32
  - 单片机
  - 嵌入式
  - 电子工程
  - 硬件设计
date: 2016-11-16 20:34:56
---

        STM32单片机支持单线半双工的USART通讯方式，在Dynamixel 家族例如AX-12、RX-64等舵机中应用较多。

        以下内容节选自为官方数据手册中文版▼：

> 单线半双方模式通过设置USART_CR3寄存器的HDSEL位选择。在这个模式里，下面的位必须保持清零状态： ● USART_CR2寄存器的**LINEN**和**CLKEN**位 ● USART_CR3寄存器的**SCEN**和**IREN**位
> 
> USART可以配置成遵循单线半双工协议。在单线半双工模式下，TX和RX引脚在芯片**内部互连**。使用控制位”HALF DUPLEX SEL”(USART_CR3中的HDSEL位)选择半双工和全双工通信。
> 
> 当HDSEL为’1’时（注：半双工模式下） ● RX不再被使用 ●  当没有数据传输时，**TX总是被释放**。因此，它在空闲状态的或接收状态时表现为一个标准I/O口。这就意味该I/O在不被USART驱动时，必须配置成**悬空输入**(**或开漏的输出高**)。除此以外，通信与正常USART模式类似。由软件来管理线上的冲突(例如通过使用一个中央仲裁器)。特别的是，发送从不会被硬件所阻碍。当 TE位被设置时，只要数据一写到数据寄存器上，发送就继续。

        重点放在：开漏输出高/OD门高电平

        认识一下推挽输出和开漏输出▼：

![output_ppod](http://oarap.org/wp-content/uploads/2016/11/OUTPUT_PPOD.png)

        上图中左侧电路为推挽输出，推挽输出非常形象：一推一拉驱动后端负载，同一时刻只能有一个MOS管导通，右侧电路为开漏输出（也称OD门 Open Drain），OD/OC门如果不加上拉电阻在输出端是没有电平表现出来的，另外一个特点就是：线与。

        如果在推挽输出的情况下，直接叠加电平到推挽电路的输出口极有可能导致损坏MOS管，而OD/OC门如果叠加电平在输出口将实现的是电平的与操作，所以在单线半双工这种一根线上两侧都有输出权利的时候，线与对器件的保护就凸显出来了。

        下图是STM32的GPIO结构图▼：

![stm32_gpio](http://oarap.org/wp-content/uploads/2016/11/STM32_GPIO.png) ![stm32_gpio_output_config](http://oarap.org/wp-content/uploads/2016/11/STM32_GPIO_OUTPUT_CONFIG.png)

        可以看到，芯片通过激活或关闭P-MOS管来实现推挽和开漏的电路功能。

#####         最重要的就是：如果设置了STM32开漏输出高，芯片会关闭P-MOS形成开漏电路，但是相比之前提到的OD门电路少了一个**上拉电阻**，如果没有上拉电阻，OD门是不能工作的，所以一定要注意在数据脚上拉电阻到VCC，这是数据手册中没有说明的。

        ▼以下为USART2的初始化代码，供诸位调试参考：

GPIO\_InitStructure.GPIO\_Pin = GPIO\_Pin\_2;
GPIO\_InitStructure.GPIO\_Mode = GPIO\_Mode\_AF_OD;  //开漏输出模式
GPIO\_InitStructure.GPIO\_Speed = GPIO\_Speed\_50MHz;
GPIO\_Init(GPIOA, &GPIO\_InitStructure);
GPIO\_SetBits(GPIOA,GPIO\_Pin_2);                 //置高
USART\_InitStructure.USART\_BaudRate = 9600;
USART\_InitStructure.USART\_WordLength = USART\_WordLength\_8b;
USART\_InitStructure.USART\_StopBits = USART\_StopBits\_1;
USART\_InitStructure.USART\_Parity = USART\_Parity\_No;
USART\_InitStructure.USART\_HardwareFlowControl = USART\_HardwareFlowControl\_None;
USART\_InitStructure.USART\_Mode = USART\_Mode\_Rx | USART\_Mode\_Tx;
USART\_Init(USART2, &USART\_InitStructure);
USART\_ITConfig(USART2,USART\_IT_RXNE,ENABLE);
USART_Cmd(USART2, ENABLE);
USART_HalfDuplexCmd(USART2,ENABLE);              //半双工

        ▼下图为STM32单片机和AX-12舵机单线半双工通信读取舵机温度时的波形，供诸位调试参考。

![ax-12_wave](http://oarap.org/wp-content/uploads/2016/11/AX-12_WAVE.png)        

* * *