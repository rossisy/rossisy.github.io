---
layout: post
title: "File Search Linux"
date: 2018-02-20 22:00:00 +0800
categories: Linux
---
# File Search
## 脚本文件名查询
### which(shows the full path of (shell) commands)
**常用参数:**
    -a: 将所有由PATH目录中可以找到的可执行命令均列出

### type

## 文件名查找
### whereis(locate the binary, source, and manual page files for command)
**常用参数:**
    -b: 只找二进制格式的文件
    -m: 只找在说明文件manual路径下的文件
    -s: 只找source源文件
    -u: 查找不在上述三个选项中的其他特殊文件

### locate
**常用参数:**
    -i: 忽略大小写的差异
    -r: 接正则表达式的显示方式

whereis和locate都是使用Linux中的记录文件的数据库进行查询的，所有查询速度较快但在时效性上有限制。默认情况下该数据库每天更新一次，更新后新增的文件无法通过这两个命令查到，若想手动更新该数据库可以使用updatedb命令。

### find(search for files in a directory hierarchy)
**常用参数:**
    -mtime n: n为数字，意义为在n天之前的“一天之内”被更改过的文件
    -mtime +n: 列出在n天之前（不含n天本身）被更改过的文件名
    -mtime -n: 列出n天之内（含n天本身）被更改过的文件名
    -newer file: file为一个存在的一天文件，列出比file还要新的文件名
    -uid n: n为数字，这个数字是用户的账号ID，即UID
    -gid n: n为数字，这个数字是用户组的ID，即GID
    -user name: name为用户账号名称
    -group name: name为用户组名
    -nouser: 寻找文件的所有者不存在于/etc/passwd的文件
    -nogroup: 寻找文件的用户组不存在于/etc/group中的文件
    -name filename: 查找文件名为filename的文件
    -size [+-]SIZE: 查找比SIZE还要大（+）或小（-）的文件。
    -type TYPE: 查找文件的类型为TYPE的，类型主要有：一般正规文件（f）、设备文件（b，c）、目录（d）、连接文件（l）、socket（s）及FIFO（p）等属性
    -perm mode: 查找文件权限“刚好等于”mode的文件，这个mode为类似chmod的属性值
    -perm -mode: 查找文件权限“必须要全部包括mode的权限”的文件
    -perm +mode: 查找文件权限“包含任一mode的权限”的文件
    -exec command: -exec后接其他命令来处理查找到的结果

