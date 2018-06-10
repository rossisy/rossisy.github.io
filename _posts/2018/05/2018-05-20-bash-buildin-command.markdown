---
layout: post
title: "bash build-in commands"
date: 2018-05-20 10:00:00 +0800
categories: shell
---
# bash shell内置命令
shell中使用的命令可以分为shell内置的命令yu非shell提供的命令两种。

## type
查询命令的类型与信息

type [-tpa] command
不加任何参数时，type命令会显示command是内置的还是非内置的命令

-t:
type会将command以下面内容显示其意义：
    file：表示为外部命令
    alias：表示该命令为命令别名所设置的名称
    builtin：表示该命令为bash内置的命令功能

-p:
如果command为外部命令时，才会显示完整文件名

-a:
将PATH变量定义的路径中所有含command的命令都列出来，包含alias

## echo
将参赛写入标准输出

## export
将shell变量或函数输出为环境变量

## unset
删除已定义的shell变量（包括环境变量）和shell函数。unset命令不能够删除具有只读属性的shell变量和环境变量。

## read
从键盘读取变量的值，通常用在shell脚本中与用户进行交互的场合。可以一次读取多个变量的值，变量和输入的值都需要使用空格隔开。在read命令后，如果没有指定变量名，读取的数据将被自动赋值给特定的变量REPLY。

read [-pt] variable
-p:
使用指定的提示符

-t:
等待时间（s）

## declare / typeset
声明变量的类型

declare [-aixr] variable
不接任何参数时，显示所有变量名称与内容

-a:
将后面名为variable的变量定义成为数组（array）类型

-i:
将后面名为variable的变量定义成为整数数字（integer）类型

-x:
用法与export一样，就是将后面的variable变成环境变量

-r:
将变量设置成为readonly类型，该变量不可被更改内容，也不能重设

-p:
单独列出变量的类型

## ulimit
用于限制系统用户对shell资源的访问

ulimit [-SHacdfltu] [配额]

-H:
严格的设置，必定不能超过这个设置的数值

-S:
警告的设置，可以超过这个设置值，若超过则有警告信息

-a:
后面不接任何参数，可列出所有的限制设置

-c:
当某些进程发生错误时，系统可能会将该进程在内存中的信息写成文件（拍错用）

-f:
此shell可以创建的最大文件容量，单位是KB

-d:
进程可使用的最大数据节区（segment），单位是KB

-l:
可以用于锁定的内存量

-t:
可使用的最大CPU时间，单位是秒

-u:
单一用户可以使用的最大进程数

# 变量内容的删除与替换

|方式|说明|
|:-:|:-:|
|${变量#关键字}|若变量内容从头开始的数据符合“关键字”，则将符合的最短数据删除|
|${变量##关键字}|若变量内容从头开始的数据符合“关键字”，则将符合的最长数据删除|
|${变量%关键字}|若变量内容从尾向前的数据符合“关键字”，则将符合的最短数据删除|
|${变量%%关键字}|若变量内容从尾向前的数据符合“关键字”，则将符合的最长数据删除|
|${变量/旧字符串/新字符串}|若变量内容符合“旧字符串”，则将第一个旧字符串替换成新字符串|
|${变量//旧字符串/新字符串}|若变量内容符合“旧字符串”，则将全部旧字符串替换成新字符串|

# 变量测试与赋值
newVar=${oldVar-default}
如果oldVar不存在（未赋值），则将default的值赋给newVar，否则将oldVar的值赋给newVar

newVar=${oldVar:-default}
如果oldVar不存在（为赋值）或为空，则将default的值赋给newVar，否则将oldVar的值赋给newVar

|方式|str没有设置|str为空字符串|str为非空字符串|
|:-:|:-:|:-:|:-:|
|var=${str-expr}|var=expr|var=|var=$str|
|var=${str:-expr}|var=expr|var=expr|var=$str|
|var=${str+expr}|var=|var=expr|var=expr|
|var=${str:+expr}|var=|var=|var=expr|
|var=${str=expr}|var=expr,str=expr|var=,str不变|var=$str,str不变|
|var=${str:=expr}|var=expr,str=expr|var=expr,str=expr|var=$str,str不变|
|var=${str?expr}|expr输出至std err|var=|var=$str|
|var=${str:?expr}|expr输出至std err|expr输出至std err|var=$str|

# 命令别名
## alias
如果alias后不接任何参数，列出当前所有的alias；设置新的alias则需要在后面加上"别名"='命令参数...'

## unalias
取消命令别名

# 历史命令
## history
history [n]
history [-c]
history [-raw] histfiles
参数：
n:
数字，是要列出最近的n条命令行的意识

-c:
将目前的shell中的所有history内容全部消除

-a:
将目前新增的history命令新增入histfiles中，若未指定histfiles，则默认写入~/.bash_history

-r:
将histfiles的内容读到目前这个shell的history记忆中

-w:
将目前的history记忆内容写入histfiles中

!number
执行第几条命令

!command
由最近的命令向前搜索命令串开头为command的那个命令，并执行

!!
执行上一个命令（相当于按向上的方向键后按[Enter]


