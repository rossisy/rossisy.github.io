---
layout: post
title: "File Permission Linux"
date: 2018-02-15 15:00:00 +0800
categories: Linux
---
# File Permission
Linux一般将文件可存取访问的身份分为3个类别：owner、group、others，3种身份各有read、write、execute权限。

## 用户与用户组记录文件
用户信息: 所有系统上的账号与一般身份用户和root的相关信息都是记录在/etc/passwd中。
账户密码: 个人的密码记录在/etc/shadow中。
用户组信息: 所有的组名都记录在/etc/group中。

## 文件属性
使用ls -l命令将目录内容以long listing格式输出时，输出格式如下：
[权限][连接][所有者][用户组][文件容量][修改日期][文件名]

### 权限
第一部分用10个字符展示文件的类型与权限。第一个字符表示文件的类型，后九个字符每3个为一组分别表示文件所有者、文件所属用户组和其他人的可读、可写和可执行的权限。
第一个字符意义:

|字符|含义|
|:-:|:-:|
|d|目录|
|-|文件|
|l|链接文件（linkfile）|
|b|设备文件里可供存储的接口设备|
|c|设备文件里的串行端口设备|

权限字符意义:

|字符|含义|
|:-:|:-:|
|r|可读（read）|
|w|可写（write）|
|x|可执行（execute）|
|-|无权限|
注：文件与目录的权限意义并不相同

第二部分表示有多少文件名连接到此节点。

第三部分表示文件的所有者账号。

第四部分表示文件的所属用户组。

第五部分为文件的容量大小，默认单位为B。

第六部分为文件的创建文件日期或最近修改的修改日期。

第七部分为文件名。

#### 修改文件属性与权限
chgrp: 改变文件所属用户组。
chown: 改变文件所有者。
chmod: 改变文件的权限。

chgrp:
chgrp [OPTION]... GROUP FILE...

chown:
chown [OPTION]... [OWNER][:GROUP] FILE...

chmod:
chmod [OPTION]... MODE[,MODE]... FILE...
chmod [OPTION]... OCTAL-MODE FILE...

权限修改可以使用两种方式: 符号和数字。
符号和数字表示的权限对应表如下：

|SYMBOL|NUM|
|:-:|:-:|
|r|4|
|w|2|
|x|1|
|-|0|

使用数字方式修改权限时，需要将每种身份各自的三个权限数字相加。
例：
chmod -R 755 filename

使用符号方式修改权限时，通过u,g,o,a分别代表user、group、others和all的身份，+、-和=分别表示加入、除去和设置权限，r、w、x表示可读，可写、可执行的权限。

|COMMAND|ROLE|OPERATION|PERMISSION|FILE|
|:-:|:-:|:-:|:-:|:-:|
|chmod|u,g,o,a|+,-,=|r,w,x|文件或目录|

#### 文件权限与目录权限
1. 文件权限的意义
文件的权限主要都是针对文件内容而言，意义如下：
r（read）：可读，可读取此文件的实际内容。
w（write）：可写，可编辑、新增或是修改文件内容。
x（execute）：可执行，可被系统执行。

2. 目录权限的意义
目录的权限主要都是针对目录内容（文件名列表），意义如下：
r（read contents in directory）：可读，可读取目录结构列表。
w（modify contents of directory）：可写，可更改该目录结构列表，即可以在该目录下新建文件与目录、删除文件与目录（不论该文件的权限为何）、重命名文件或目录、转移文件或目录位置。
x（access directory）：可进入，可进入该目录成为工作目录。

## 文件种类
1. 普通文件（regular file），字符[-]表示。包括纯文本（ASCII）、二进制文件（binary）、数据格式文件（data）。
2. 目录（directory），字符[d]表示。
3. 连接文件（link），字符[l]表示。
4. 块设备文件（block），字符[b]表示。
5. 字符设备文件（character），字符[c]表示。
6. 套接字（sockets），字符[s]表示。
7. 管道（FIFO，pipe），字符[p]表示。
