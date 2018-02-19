---
layout: post
title: "Man Page Linux"
date: 2018-02-11 15:00:00 +0800
categories: Linux
---
# Man Page
##  Man page里命令名称后括号里的数字意义：

|数字|含义|
|:-:|:-|
|1|用户在shell环境中可以操作的命令或可执行文件|
|2|系统内核可调用的函数与工具等|
|3|一些常用的函数（function）与函数库（library），大部分为C的函数库（lib c）
|4|设备文件的说明，通常在/dev下的文件|
|5|配置文件或者是某些文件的格式|
|6|游戏（games）|
|7|惯例与协议等，例如Linux文件系统、网络协议、ASCII code等说明|
|8|系统管理员可用的管理命令|
|9|跟kernel有关的文件|

## Man page的主要组成部分：

|部分|内容说明|
|:-:|:-|
|NAME|简短的命令、数据名称说明|
|SYNOPSIS|简短的命令执行语法（syntax）简介|
|DESCRIPTION|较为完整的说明|
|OPTIONS|针对SYNOPSIS部分中，有列举的所有可用的选项说明|
|COMMANDS|当这个程序（软件）在执行的时候，可用在此程序（软件）中执行的命令|
|FILES|这个程序或数据所使用或参考或连接到的某些文件|
|SEE ALSO|与命令或数据有相关的其他说明|
|EXAMPLE|参考的范例|
|BUGS|是否有相关的错误|
|AUTHORS|作者信息|
|COPYRIGHT|版权信息|

## Man page的常用操作

|按键|作用|
|:-:|:-|
|空格键|向下翻一页|
|[Page Down]|向下翻一页|
|[Page Up]|向上翻一页|
|[Home]|去到第一页|
|[End]|去到最后一页|
|/string|向下查询string字符串|
|?string|向上查询string字符串|
|n,N|利用/或?来查询字符串时，可以使用n来继续下一个查询（不论是/或?），可以利用N来进行反向查询。举例来说，我以/keyword查询keyword字符串，那么可以n继续往下查询，用N往上查询。若以?keyword向上查询keyword字符串，那我可以用n继续向上查询，用N反向查询|
|q|退出man page|

## Man命令常用方法
1. man -f smail
    查找man page中NAME的部分与smail一致的，并打印出简短的描述。与whatis -r smail的功能一致。
2. man -k printf
    查找manual page names和short descriptions中包含printf的，并打印出来。与apropos -r printf的功能一致。

