---
layout: post
title: "User Information Delivery"
date: 2019-01-05 10:00:00 +0800
categories: Linux 
---
# 查询用户：w, who, last, lastlog

## w
查询目前已登录的用户，显示内容包含：
第一行显示目前的时间、开机（up）多久，几个用户在系统上的平均负载等
第二行只是各列的说明
第三行以后，每行代表一个用户

## who
查询目前已登录系统的用户

## last
查询用户登录的时间

## lastlog
查询每个账号最近登录的时间，lastlog会去读取/var/log/lastlog文件，结果将数据输出

# 用户对谈：write, mesg, wall

## write
write可以直接将信息传给接收者。
write 用户账号 [用户所在终端接口]

## mesg
是否显示消息，不过mesg的功能对root传送过来的信息没有抵抗的能力
mesg [y | n]

## wall
对所有系统上的用户传送信息（广播）
wall "message"

# mail
给用户寄送邮件
mail username@localhost -s "邮件标题"
以上命令输入后，回车即可编写邮件正文，邮件正文以最后一行是小数点为结束标志。
如果有抄送的人，可以在正文结束后新起一行以Cc: 开头输入抄送人邮箱，最后用回车 结束，返回到命令提示符则表示输入完毕邮件已发出
还可以使用数据流重定向作为邮件正文，避免内容输入有误

单独使用mail命令，可以查阅邮件。在mail当中&是提示符
