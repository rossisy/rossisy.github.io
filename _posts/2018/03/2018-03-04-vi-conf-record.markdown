---
layout: post
title: "vim configuration and record"
date: 2018-03-03 10:00:00 +0800
categories: vi
---
# vim configuration and records
## vim的环境设置参数

|命令|功能|
|:-:|:-|
|:setnu与:setnonu|就是设置与取消行号|
|:sethlsearch或:setnohlsearch|hlsearch就是high light search（高亮查找）。这个就是设置是否将查找的字符串反白的设置值。默认值是hlsearch|
|:setautoindent与:setnoautoindent|表示是否自动缩进|
|:setbackup|表示是否自动保存备份文件，一般是nobackup的，如果设置backup的话，那当修改任何一个文件时，原文件会被另存为一个文件名为filename~的文件|
|:setruler|是否显示右下角的状态栏说明|
|:setshowmode|是否显示当前模式（--INSERT--之类的当前模式名字)在左下角的状态栏|
|:setbackspace=(0,1,2)|编辑状态时，backspace（退格键）设置，当backspace为2时，可以删除任意值，为0或1时，仅可以删除刚才输入的字符，无法删除原来已经存在的字符|
|:setall|显示目前所有的环境参数设置值|
|:set|显示与系统默认值不同的设置参数，一般来说就是有自行变动过的设置参数|
|:syntax on或:syntax off|表示是否依据程序相关语法显示不同颜色|
|:set bg=dark或:set bg=light|设置不同的颜色色调，默认是light|

通常总是通过vim的配置文件来设置这些环境参数，配置文件为vimrc。一般使用~/.vimrc的用户配置文件。

