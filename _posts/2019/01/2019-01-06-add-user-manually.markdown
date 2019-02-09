---
layout: post
title: "Add User manually"
date: 2019-01-06 10:00:00 +0800
categories: Linux 
---
# 一些检查工具

## pwck
检查/etc/passwd这个账号配置文件内的信息与实际的主文件夹是否存在等等信息，还可以比较/etc/passwd和/etc/shadow的信息是否一致，另外，如图/etc/passwd内的数据字段错误，会提升用户修改。

## grpck
与pwck相应，这个是检查用户组的命令

## pwconv
这个命令主要的目的是将/etc/pqsswd内的账号与密码移动到/etc/shadow当中！pwconv可以比较/etc/passwd及/etc/shadow，若/etc/passwd内存在的账号并没有对应的/etc/shadow密码时，则pwconv会去/etc/login.defs取相关的密码数据，并新建该账号的/etc/shadow数据；若/etc/passwd内存在加密后的密码数据时，则pwconv会将该密码列移动到/etc/shadow内，并将原本的/etc/passwod内相对应的密码列变成x

## pwunconv
将/etc/shadow内的密码列数据写回到/etc/passwd中，并删除/etc/shadow文件。

## chpasswd
可以读入未加密前的密码，并且经过加密后，将加密后的密码写入/etc/shadow当中。经常在批量新建账号的情况中使用该命令，它可以有标准输入中读入数据，每条数据的格式是“username:password”。
例：要更新用户dmtsai的密码为abcdefg，则
```
echo "dmtsai:abcdefg" | chpasswd -m
```
默认的情况下，chpasswd使用的是DES加密方法来加密，我们可以使用chpasswd -m来使用CentOS默认的MD5加密方式。

# 特殊账号（如纯数字账号）的手工新建
因账号与用户组是与/etc/group、/etc/shadow、/etc/passwd、/etc/gshadow有关，因此，整个操作是这样的：
1. 先新建所需要的用户组（vi /etc/group）
2. 将/etc/group与/etc/gshadow同步（grpconv）
3. 新建账号的各个属性（vi /etc/passwd）
4. 将/etc/passwd与/etc/shadow同步（pwconv）
5. 新建该账号的密码（passwd accountname）
6. 新建用户主文件夹（cp -a /etc/skel /home/accountname)
7. 更改用户主文件夹的属性（chown -R accountname:group /home/accountname）

