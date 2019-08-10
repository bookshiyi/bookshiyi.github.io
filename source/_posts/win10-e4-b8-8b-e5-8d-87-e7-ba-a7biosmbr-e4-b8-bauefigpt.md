---
title: WIN10下升级BIOS+MBR为UEFI+GPT
tags:
  - DiskGenius
  - gpt
  - mbr
  - uefi
url: 818.html
id: 818
comments: false
categories:
  - 电脑
date: 2016-05-18 18:29:38
---

        近日发现升级完win10系统后开机速度有些捉急，突然想起以前使用win7的时候还是使用的BIOS+MBR模式，遂决定将电脑升级为UEFI+GPT的模式。

        闲言少叙，首先MBR升级GPT，自备WinPE的U盘一个，需要使用软件【DiskGenius】将分区表更改为GUID类型，之前请备份好分区表，最好整盘数据都备份以防不测（由于笔者的电脑分区数多于4个，所以直接升级为GPT会导致数据的丢失，小于或等于四个分区的磁盘理论上无损从MBR转到GPT）。然后建立一个200M空间（如果是GPT请建立EFI分区，如果是MBR格式请建立FAT/FAT16分区），将这个空间格式化并分配一个盘符，然后使用UEFI引导修复工具_**[点我下载](http://oarap.org/wp-content/uploads/2016/05/BIOS_UEFI_boot_repair.rar)**_，输入系统所在的盘符和刚才建立的EFI所在分区的盘符，

![UEFI_boot_repair](http://oarap.org/wp-content/uploads/2016/05/UEFI_boot_repair.jpg)

        修复完成后就可以重新启动了（记得把BIOS里面的启动方式设为仅UEFI或者UEFI优先，不然之前的操纵就都没有意义了），系统启动方式升级完毕。

* * *