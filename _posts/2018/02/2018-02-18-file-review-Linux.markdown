---
layout: post
title: "File Review Linux"
date: 2018-02-18 22:00:00 +0800
categories: Linux
---
# File Review
## cat (concatenate files and print on the standard output)
由第一行开始显示文件内容

## tac (concatenate and print files in reverse)
从最后一行开始显示

## nl (number lines of files)
显示的时候，顺便输出行号

## more (file perusal filter for crt viewing)
一页一页地显示文件内容

## less (opposite of more)
与more类型，但可以往前翻页

## head （output the first part of files)
只显示文件的第一部分

## tail (output the last part of files)
只显示文件的最后一部分

## od (dump files in octal and other formats)
以8进制或其他格式读取文件

## touch (change file timestamps)
修改文件时间或创建新文件
Linux中文件主要有是哪个变动时间：  
    modification time (mtime): 文件内容的修改时间  
    status time (ctime): 文件状态(权限和属性)的修改时间  
    access time (atime): 文件内容读取时间

**参数:**  
    -a: 仅修改访问时间  
    -c: 不创建任何文件  
    -d: 使用字符串的日期来修改文件日期  
    -t: 使用[[CC]YY]MMDDhhmm[.ss]格式的时间来修改文件  
    -m: 修改mtime
