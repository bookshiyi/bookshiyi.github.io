---
title: 开机自动连接蓝牙的shell
url: 1546.html
id: 1546
categories:
  - 建站
tags:
---

**1、首先编写一个简单的shell脚本** vim test.sh(不习惯使用vim可以使用nano) 进入vim后按i键,然后输入（#!/bin/sh符号#!用来告诉系统它后面的参数是用来执行该文件的程序。） **#!/bin/bash ** **echo "Hello world!"** **filename=\`date "+%Y%m%d"\` ** **echo $filename** 然后先Esc再shift+z两次（保存） 在命令行输入：chmod +x test.sh(赋予执行权限) 运行：./test.sh **查看命令的路径：which ls(假设查看ls命令的路径)** **#后面的内容表示注释，要养成写注释的良好习惯** [更多shell编程知识](http://wiki.ubuntu.org.cn/Shell%E7%BC%96%E7%A8%8B%E5%9F%BA%E7%A1%80#.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.8F.82.E6.95.B0)        ** [shell编程简介](http://net.pku.edu.cn/%7Eyhf/tutorial/shellProgramIntro.htm)** **2、设置脚本开机自启动** **只需编辑/etc/init.d/rc.local文件，在最后加上你的脚本即可。** **比如：我已经编写了一个脚本apk.sh,存放在/home/apk/ 下面** **在Ubuntu终端输入 sudo  nano  /etc/init.d/rc.local编辑文件，在结尾出加入：** **/home/apk/shell.sh 即可开机自动加载脚本。** **--------------------或者使用下面的方法------------------** **1) 将你的启动脚本复制到 /etc/init.d目录下** **sudo  cp  test.sh  /etc/init.d/**   **2) 执行如下命令将脚本放到启动脚本中去：** **$ cd /etc/init.d** **$ sudo chmod 755 /etc/init.d/test.sh** **$ sudo update-rc.d test.sh defaults 95** 注：其中数字95是脚本启动的顺序号，按照自己的需要相应修改即可。在你有多个启动脚本，而它们之间又有先后启动的依赖关系时你就知道这个数字的具体作用了。该命令的输出信息参考如下： update-rc.d: warning: /etc/init.d/test missing LSB information update-rc.d: see   **卸载启动脚本的方法：** $ cd /etc/init.d   $ sudo update-rc.d -f test.sh remove **注意事项：** **开始我使用forever命令写了一个脚本，如下：** **#!/usr/local/bin/forever** **    forever start /home/apk/apkAnalysis/app.js** **可是不论我使用什么方法它都启动不起来，后来发现它少了一个sudo权限：** **    #!/usr/local/bin/forever** **    sudo forever start /home/apk/apkAnalysis/app.js** 所以在配置开机启动的时候一定要注意**sudo**的使用 查看系统启动的日志：**cat /var/log/boot.log ** 开始是一直都起不来，看了下日志，发现文件不存在;登录之后查看文件是存在的，可能是执行启动脚本的时候用户目录还没有mount上来 **然后把工程放到srv目录下面就可以开机自启动了。** **改一下权限****sudo chmod 775 /srv/**            

[Ubuntu 16.04添加开机启动脚本的方法](http://blog.csdn.net/sinat_36219858/article/details/61195905)
=======================================================================================

2017-03-10 13:22 6人阅读 [评论](http://blog.csdn.net/sinat_36219858/article/details/61195905#comments)(0) 收藏 [举报](http://blog.csdn.net/sinat_36219858/article/details/61195905#report "举报")

![](http://oarap.org/wp-content/uploads/2017/03/category_icon.jpg)分类：

ubuntu16.04_（8）_ ![](http://oarap.org/wp-content/uploads/2017/03/arrow_triangle20_down.jpg) 

A 自带开机脚本 /etc/rc.local脚本是一个ubuntu16.04及其以前的系统中自带的开机脚本，在没有修改之前里面内容如下。

`#!/bin/sh -e`

`#`

`# rc.local`

`#`

`# This script is executed at the end of each multiuser runlevel.`

`# Make sure that the script will "exit 0" on success or any other`

`# value on error.`

`#`

`# In order to enable or disable this script just change the execution`

`# bits.`

`#`

`# By default this script does nothing.`

`exit` `0 可以把开机要执行的命令放到 exit0 前面。` **B 添加开机脚本** **1,新建个脚本文件new_service.sh**

1

2

3

4

`#!/bin/bash`

`# command content`

`exit` `0`

**2,设置权限**

1

`sudo` `chmod` `755 new_service.sh`

**3,把脚本放置到启动目录下**

1

`sudo` `mv` `new_service.sh` `/etc/init``.d/`

**4,将脚本添加到启动脚本** 执行如下指令，在这里90表明一个优先级，越高表示执行的越晚

1

2

`cd` `/etc/init``.d/`

`sudo` `update-rc.d new_service.sh defaults 90`

**移除Ubuntu开机脚本**

1

`sudo` `update-rc.d -f new_service.sh remove`