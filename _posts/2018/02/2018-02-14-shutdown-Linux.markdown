---
layout: post
title: "shutdown Linux"
date: 2018-02-14 15:00:00 +0800
categories: Linux
---
# shutdown
Linux中与关机/重启相关的几个命令：
数据同步写入硬盘的命令：sync
惯用的关机命令：shutdown
重启、关机：reboot，halt，poweroff

## sync
用于将内存中尚未被更新的数据写人硬盘中。

## shutdown
shutdown [OPTIONS...] [TIME] [WALL...]
OPTIONS:
    -t sec : -t 后面加秒数，也即“过几秒后关机”的意思
    -k : -k 不关机，只是发送警告消息出去
    -r : 在将系统的服务停掉之后就重启（常用）
    -h : 将系统的服务停掉后，立即关机（常用）
    -n : 不经过init程序，直接以shutdown的功能来关机
    -f : 关机并开机之后，强制略过fsck的磁盘检查
    -F : 系统重启之后，强制进行fsck的磁盘检查
    -c : 取消已经在进行的shutdown命令内容

## reboot
reboot [OPTIONS...]

## halt
halt [OPTIONS...]

## poweroff
poweroff [OPTIONS...]

## init
切换执行等级。
init [OPTIONS...] {COMMAND}
Linux共有7种执行等级，init命令可用的有其中的4种：
run level 0: 关机
run level 3: 纯命令行模式
run level 5: 含有图形界面模式
run level 6: 重启
使用init命令来关机:
```
[root@localhost ~]# init 0
```
