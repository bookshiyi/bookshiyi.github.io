---
title: Ubuntu下解决SSH链接中文乱码
tags:
  - FTP
  - linux
  - SSH
  - Ubuntu
  - UTF-8
  - 乱码
url: 1515.html
id: 1515
comments: false
categories:
  - Linux
  - 互联网
  - 信息技术
  - 开源
  - 开源软件
date: 2017-02-25 17:19:49
---

     原因分析：由于ubuntu系统默认是utf-8，而我们用SecureCRT打开的编码是gbk，包括使用基于SSH的FTP工具FlashFXP等大多使用gbk编码，当浏览一个带有中文的文件/命令就会出现乱码。

#### **    方法A：**

       在linux的当前用户目录后，输入ls -a查看隐藏的文件，则会有一个.profile或者.bash\_profile，Ubuntu下是.profile，其他linux可能是.bash\_profile，修改如下：

\# ~/.profile: executed by Bourne-compatible login shells.
if \[ "$BASH" \]; then
if \[ -f ~/.bashrc \]; then
. ~/.bashrc
fi
fi
mesg n
#在最末尾添加下面两行代码：
LANG=zh_CN.GB2312
export LANG

#### **    方法B：**

        修改本地的SSH客户端的语言使其和远程服务器的语言一致，不同客户端的设置方法不尽相同，具体步骤不再赘述。