---
title: 树莓派3B+在Ubuntu MATE环境下配置VNC
url: 1520.html
id: 1520
categories:
  - 建站
tags:
---

安装vnc 配置vnc 设置开机启动 Ubuntu15.04： Ubuntu15.04以后得服务管理器已经切换到了systemd中，其系统服务脚本目录为：/lib/systemd/system/ 所以要自动启动x11vnc，需要在系统服务目录中新建服务文件 sudo vi /lib/systemd/system/x11vnc.service 拷贝下面的内容到文件中： \[Unit\] Description=Start x11vnc at startup. After=multi-user.target \[Service\] Type=simple ExecStart=/usr/bin/x11vnc -auth guess -forever -loop -noxdamage -repeat -rfbauth /home/USERNAME/.vnc/passwd -rfbport 5900 -shared \[Install\] WantedBy=multi-user.target 然后以754的权限保存在根目录： sudo chmod 774 /lib/systemd/system/x11vnc.service 然后再设置二开机自启服务： sudo systemctl enable x11vnc.service