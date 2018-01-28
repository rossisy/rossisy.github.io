---
layout: post
titil: "Hardware in Linux"
date: 2018-01-28 22:11:00 +0800
categories: Linux
---

# 常见硬件在Linux中的表示
计算机常见硬件设备的Linux文件表示如下：

|设备|Linux的文件名|
|:-:|:-:|
|SCSI/SATA/USB硬盘|/dev/sd[a-p]|
|U盘|/dev/sd[a-p]\(与SATA相同\)|
|打印机|25针: /dev/lp[0-2]<br>USB: /dev/usb/lp[0-15]|
|鼠标|USB: /dev/usb/mouse[0-15]<br>PS2: /dev/psaux|
|当前鼠标|/dev/mouse|
|当前CD ROM/DVD ROM|/dev/cdrom|
|~~IDE硬盘~~|/dev/hd[a-d]|
|~~软驱~~|/dev/fd[0-1]|
|~~磁带机~~|IDE: /dev/ht0<br>SCSI: /dev/st0|

更多Linux支持的硬件可以参见如下网址的内容
https://www.kernel.org/pub/linux/docs/lanana/device-list/

# 硬盘在Linux中的具体文件名
## 1. IDE硬盘
|IDE|Master|Slave|
|:-:|:-:|:-:|
|IDE1(Primary)|/dev/hda|/dev/hdb|
|IDE2(Secondary)|/dev/hdc|/dev/hdd|

## 2. SATA&USB硬盘
因为SATA/USB/SCSI等硬盘接口都是使用SCSI模块来驱动的，所以这些接口的硬盘设备文件名都是/dev/sd[a-p]的格式。而SATA/USB硬盘的文件名是根据Linux内核检测到的硬盘的顺序来确定的。
Linux内核检测的顺序是从SATA插槽到USB接口的，即SATA接口的硬盘的排序要在USB接口的硬盘之前。
例：SATA1>SATA2>SATA3>...>SATAn>USB1>USB2>...>USBn，如果计算机有2个SATA硬盘和2个USB硬盘，分别安装在SATA3，SATA5和USB2，USB4，他们在Linux中的设备文件名为/dev/sda，/dev/sdb，/dev/sdc，/dev/sdd
