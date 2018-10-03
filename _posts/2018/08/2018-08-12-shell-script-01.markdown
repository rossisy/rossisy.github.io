---
layout: post
title: "shell script 01"
date: 2018-08-12 10:00:00 +0800
categories: shell
---
# shell script注意事项：
1. 命令的执行是从上而下、从左而右地分析与执行
2. 命令、参数间的多个空白都会被忽略
3. 空白行也会被忽略，并且[tab]按键所得到的空白同样视为空格键
4. 如果读取到一个Enter符号(CR)，就尝试开始执行该行命令
5. 如果一行的内容太多，可以使用“\[Enter]”来扩展至下一行
6. “#”可作为批注，任何加在#后的数据将全部被视为批注文字而被忽略

# shell script执行
.sh文件必须要具备可读与可执行的权限。
1. 绝对路径：使用/path/to/shell.sh来执行
2. 相对路径：假设shell.sh在当前工作目录下，则使用./shell.sh来执行
3. 利用变量“PATH”：将shell.sh放在PATH指定的目录内，则可以直接执行shell.sh
4. 利用bash进程：通过“bash shell.sh”或“sh shell.sh”来执行

# shell script结构
```
#! /bin/bash
# Program:
#       This program shows "Hello World!" in your screen.
#History:
#2005/08/23 First release
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH
echo -e "Hello World!\a\n"
exit 0
```
## 声明script使用的shell
#! /bin/bash
使用/bin/bash，即当程序执行时，加载bash的相关环境配置文件（一般就是non-login shell的~/.bashrc），并且执行bash来使下面的命令能够执行。

## 程序内容说明
2~5行，说明程序的基本信息

## 环境变量声明
设置重要的环境变量PATH、LANG

## 主程序部分
echo哪一行

## 返回执行结果
使用exit在程序执行完后回传0给系统

# shell script执行方式的区别
利用直接执行的方式来执行script，该script都会使用一个新的bash环境来执行脚本内的命令
利用source来执行命令，该script会在当前的bash进程中执行

# test命令
test命令的标志：

|测试的标志|代表意义|
|:-:|:-:|
|关于某个文件名的“文件类型”判断，如test -e filename表示是否存在|
|-e|该文件名是否存在（常用）|
|-f|该文件名是否存在且为文件（file）（常用）|
|-d|该文件名是否存在且为目录（directory）（常用）|
|-b|该文件名是否存在且为一个block device设备|
|-c|该文件名是否存在且为一个character device设备|
|-S|该文件名是否存在且为一个Socket文件|
|-p|该文件名是否存在且为一个FIFO（pipe）文件|
|-L|该文件名是否存在且为一个连接文件|
|关于文件的全新检测，如test -r filename表示可读否（但root全新常有例外）|
|-r|检测该文件名是否存在且具有“可读”的权限|
|-w|检测该文件名是否存在且具有“可写”的权限|
|-x|检测该文件名是否存在且具有“可执行”的权限|
|-u|检测该文件名是否存在且具有“SU ID”的属性|
|-g|检测该文件名是否存在且具有“SG ID”的属性|
|-k|检测该文件名是否存在且具有“Sticky bit”的属性|
|-s|检测该文件名是否存在且为“非空白文件”|
|两个文件之间的比较，如：test file1 -nt file2|
|-nt|（newer than）判断file1是否比file2新|
|-ot|（older than）判断file1是否比file2旧|
|-ef|判断file1与file2是否为同一文件，可用在判断hard link的判定上。主要意义在于判定两个文件是否均指向同一个inode|
|关于两个整数之间的判定，例如test n1 -eq n2|
|-eq|两数值相等（equal）|
|-ne|两数值不等（not equal）|
|-gt|n1大于n2（greater than）|
|-lt|n1小于n2（less than）|
|-ge|n1大于等于n2（greater than or equal）|
|-le|n1小于等于n2（less than or equal）|
|判定字符串的数据|
|test -z string|判定字符串是否为0，若string为空字符串，则为true|
|test -n string|判定字符串是否非为0，若string为空字符串，则为false。则：-n也可省略|
|test str1 = str2|判定str1是否等于str2，若相等，则回传true|
|test str1 != str2|判定str1是否不等于str2，若相等，则回传false|
|多重条件判定，例如：test -r filename -a -x filename|
|-a|两个条件同时成立！例如test -r file -a -x file，则file同时具有r与x权限时，才回传true|
|-o|任何一个条件成立！例如test -r file -o -x file，则file具有r或x权限时，就可回传true|
|!|反向状态，如test ! -x file，当file不具有x时，回传true|

# 判断符号[]
使用判断符号的中括号需要特别注意，中括号的两端需要空格符来分隔。假设空格用< >来表示，那么这些地方需要有空格键：
[ "$HOME" == "$MAIL" ]
在中括号[]内的每个组件都需要有空格键来分隔；
在中括号内的变量，最好都以双引号括起来；
在中括号内的常量，最好都以单引号或双引号括起来

# shell script的默认变量
shell script中使用$0/$1/$2...作为变量名来表示shell中命令的参数，其中$0表示所执行的命令（即脚本路径），$1为命令的第一参数，$2为命令的第二个参数，等等
除了数字的变量外，还有些较为特殊的变量可以在script中使用来调用这些参数。
$#：代表后接的参数个数
$@：代表"$1"、"$2"、"$3"、"$4"之意，每个变量是独立的（用双引号括起来）
$*：代表"$1c$2c$3c$4"，其中c为分隔字符，默认为空格键。
shift: 参数变量号码偏移。默认是拿掉第1个参数，如果shift后接数字，则代表拿掉前几个参数的意思。

