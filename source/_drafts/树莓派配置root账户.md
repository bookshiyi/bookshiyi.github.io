---
title: 树莓派配置root账户
url: 1529.html
id: 1529
categories:
  - 建站
tags:
---

sudo passwd root更改密码 然后在 /etc/lightdm/lightdm.conf中开启root 然后把~/user/.profile拷贝到root文件夹下