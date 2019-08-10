---
title: Ubuntu下SVN服务器的搭建及常见问题
tags:
  - svn
  - Ubuntu
  - 版本控制系统
url: 1089.html
id: 1089
comments: false
categories:
  - 嵌入式
  - 软件设计
date: 2016-09-18 19:46:26
---

        笔者身处嵌入式开发领域，对于版本控制系统并不够了解，但随着硬盘中的代码越来越多，也开始担心哪天硬盘如果崩溃那我也就崩溃了，另外也是可以及时的备份代码以方便在未来退回到过去的时间点，告别低端臃肿的压缩复制备份的方式。

        至于为什么选择svn而没有使用git，是因为在笔者目前认为svn上手比较快，git上太多的功能用不到，因为我使用版本控制系统的主要目的是能及时、高效、安全的备份代码。

##### 0x00.首先有一个安装了ubuntu系统的电脑或服务器，可以处于公网或局域网（取决于你对工作范围及安全性的要求）。

##### 0x01.在服务器端安装SVN：

sudo apt-get install subversion

##### 0x02.创建一个名为SVN的文件夹，作为代码仓库的存储位置：

sudo mkdir /home/svn

##### 0x03.指定SVN在此文件夹建立代码仓库：

sudo svnadmin create /home/svn

##### 0x04.此时在/svn目录下已经创建了代码仓库的相关文件，其中的conf文件夹是我们需要特别关注的，在/home/svn/conf文件夹中，我们需要编辑以下三个文件：1.authz 用户权限； 2.passwd 用户及密码； 3.svnserve.conf 主配置文件。

> ###### 编辑svnserve.conf文件，将以下参数定义前的“#”（注释符）去掉：
> 
> \[general\]
> anon-access = read        #匿名访问权限，默认read
> auth-access = write        #认证用户权限
> password-db = passwd         #用户信息存放文件，默认在版本库/conf下面，也可以绝对路径指定文件位置
> authz-db = authz
> 
> ###### 编辑passwd文件：
> 
> \[users\]
> blade = 123        #左侧为用户，右侧为密码
> 
> ###### 编辑authz文件：
> 
> \[groups\]        #定义用户组
> admin = blade        #定义用户blade属于用户组admin
> @admin = rw        #定义隶属于用户组admin的用户都具有rw权
> \* = r         #定义任何用户都具有读取权利

##### 0x05.启动SVN服务：

sudo svnserve -d -r /home/svn

##### 0x06.通过监听3690端口，确定SVN服务是否启动成功：

sudo netstat -antp |grep svnserve

>         正常启动的结果类似如下代码：
> 
> `tcp 0 0 0.0.0.0:3690 0.0.0.0:* LISTEN 28967/svnserve`

##### 0x07.在服务器端本地测试是否可用：

sudo svn checkout svn://oarap.org           #oarap.org换成你服务器所在的地址

##### 0x08.返回结果：

>         如果在authz文件中设置了任何用户都可读，那么此时会返回一个版本号（通常是0）
> 
> `Checked out revision 0.`
> 
>         如果之前未设置任何用户可读，则此时会要求输入用户名密码，用户名密码输入正确后会提示是否记住密码。 `Store password unencrypted (yes/no)?`
> 
>         如果结果不是以上两种，通常会提供错误代码，可通过搜索错误代码确定问题所在。

##### 0x09.接下来在客户端上进行远程测试，客户端如果是ubuntu在安装了svnserve后，运行0x07步骤的命令即可。

##### 0X0A.如果客户端是windows平台可使用名为TortoiseSVN的图形界面，如果客户端在Ubuntu平台有一个名为RapidSVN的GUI软件（可以在Ubuntu软件中心找到）。

 

* * *

### Q&A

##### Q1：如何清除已经记住的密码？

##### A1：清除在系统缓存中的密码，运行如下代码：

rm -rf ~/.subversion/auth

##### Q2：需要杀死进程怎么办？

##### A2：运行如下代码：

sudo pkill svnserve

##### Q3：本地可用远程被禁止

##### A3：说明极有可能是因为被服务器的防火墙所屏蔽，我们不建议完全关防火墙，可以在服务器端运行如下代码，仅打开SVN的通信端口：

sudo ufw allow svn

##### Q4：如何让服务器开机启动SVNServe？

##### A4：将如下代码添加到/etc/rc.local中（且在exit 0这句话之前）

sudo svnserve -d -r /home/svn        #每次开机都会执行本条命令

##### Q5：显示 “连接服务器失败，你想使用缓存中的数据吗？选项：立即离线、永远离线、取消。”无法从服务器查询到日志，应该怎么解决？

##### A5：将svnserve.conf中的anon-access=**read** 改为anon-access=**none**即可。

   

* * *