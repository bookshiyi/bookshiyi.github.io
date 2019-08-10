---
title: ftp开启root账户
url: 1532.html
id: 1532
categories:
  - 建站
tags:
---

一般linux系统装的都是vsftp工具，默认情况下都不能用root账户通过ftp登录主机的，但是可以通过更改vsftp的配置文件来使得可以使用root账户登录ftp： 在/etc/vsftpd目录下找到ftpusers的配置文件(有的主机这个文件是在/etc目录下的)：

`[xuwangcheng14@root]``# more ftpusers`

`# /etc/ftpusers: list of users disallowed FTP access. See ftpusers(5).`

`root`

`daemon`

`bin`

`sys`

`sync`

`games`

`man`

`lp`

`mail`

`news`

`uucp`

`nobody`

ubuntu 16.04

linux机器下

/etc/ftpusers

注释掉 root用户就可以ftp了

这个文件上的用户名都是禁止登录ftp的，将文件中的root注释掉，然后重启下vsftp服务就可以了。