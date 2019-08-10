---
title: 使用VNC实现linux与win之间剪切板传递
tags:
  - linux
  - vnc
  - 剪切板
url: 1522.html
id: 1522
comments: false
categories:
  - Linux
  - 开源软件
date: 2017-04-14 11:32:13
---

 

假设目标主机是linux，终端主机是windows（在windows上使用VNC登陆linux）

**在linux中执行 vncconfig -nowin&**

*   在linux选中文字后，无需其他按键，直接在windows中可以粘贴。
*   在windows中选中文字，Ctrl+C，在linux中按中键粘贴。

 

具体表现为VNC config出现后，就可以按照上面说的进行复制粘贴了：

![](http://oss.bookshiyi.com/photo/2017/03/vnc_linux_win.jpg-high)

参考：

https://my.oschina.net/cloudcoder/blog/204822

 

* * *