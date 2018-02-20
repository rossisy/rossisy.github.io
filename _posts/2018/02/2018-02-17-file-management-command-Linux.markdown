---
layout: post
title: "Command For File Management"
date: 2018-02-17 22:00:00 +0800
categories: Linux
---
# File Management Command
## ls (list directory contents)
**常用参数:**
    -a: 全部文件，连同隐藏文件一起列出来
    -A: 列出全部文件，但不包括.和..这两个目录
    -d: 仅列出目录本身，而不是目录内的文件
    -h: 将文件容量以人类较易读的方式列出来
    -i: 列出inode号码
    -l: 列出长数据串，包含文件的属性与权限等数据
    -n: 列出UID与GID
    -r: 将排序结果反向输出
    -S: 以文件容量大小排序
    -t: 依时间排序
    --full-time: 以完整时间模式输出

## cp (copy files and directories)
**常用参数:**
    -a: 相当于-dR
    -d: 若源文件为连接文件则复制连接文件属性而非文件本身
    -R, -r: 递归复制，用于目录的复制
    -f: 若目标文件已存在且无法打开，则删除后再尝试一次
    -i: 若目标文件已存在，在覆盖时会先提示
    -l: 创建硬连接文件
    -p: 连同文件的属性一起复制，而非使用默认属性
    -s: 复制成符号链接文件(symbolic link)
    -u: 若目标文件比源文件旧才更新目标文件

## rm (remove files or directories)
**常用参数:**
    -f: 忽略不存在的文件，不出现提示信息
    -i: 删除前询问用户
    -r: 递归删除目录及其内容

## mv (move (rename) files)
**常用参数:**
    -f: 如果目标文件已经存在，不会询问而直接覆盖
    -i: 如果目标文件已经存在，覆盖前询问
    -u: 若目标文件已经存在且源文件比较新，才会更新

## rename (rename files)
**常用参数:**
    -s: 重命名软连接

## basename (strip directory and suffix from filenames)

## dirname (strip last component from file name)

