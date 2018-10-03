---
layout: post
title: "formatting"
date: 2018-08-05 10:00:00 +0800
categories: shell
---

# 格式化打印: printf
printf '打印格式' 实际内容
参数：
	格式的样式：
		\a	警告声音输出
		\b	退格键（backspace）
		\f	清除屏幕（form feed）
		\n	输出新的一行
		\r	亦即Enter按键
		\t	水平的[tab]按键
		\v	垂直的[tab]按键
		\xNN	NN为两位数的数字，可以转换数字成为字符
	关于C程序语言内，常见的变量格式
		%ns	n是数字，s代表string，即多少个字符
		%ni	n是数字，i代表integer，即多少整数数字
		%N.nf	n与N都是数字，f代表float，如果有小数，假设共有十位数，小数点后有两位，即为%10.2f

# 数据处理工具：awk
awk '条件类型1 {动作1} 条件类型2 {动作2} ...' filename
awk的内置变量：

|变量名称|代表意义|
|:-:|:-:|
|NF|每一行（$0）拥有的字段总数|
|NR|目前awk所处理的是“第几行”数据|
|FS|目前的分割字符，默认是空格键|

awk的逻辑运算符：

|运算符|代表意义|
|:-:|:-:|
|>|大于|
|<|小于|
|>=|大于或等于|
|<=|小于或等于|
|==|等于|
|!=|不等于|

# 文件比较工具
## diff
diff [-bBi] from-file to-file
参数：
	from-file: 一个文件名，作为欲比较文件的文件名
	to-file：一个文件名，作为目的比较文件的文件名
	注意，from-file或to-file可以用-替换，那个-代表“Standardinput”之意
	-b：忽略一行当中仅有多个空白的区别（例如“about me” 与“about    me”视为相同）
	-B：忽略空白行的区别
	-i：忽略大小写的不同

## cmp
cmp [-s] file1 file2
参数：
	-s：将所有的不同点的字节处都列出来。因为cmp默认仅会输出第一个发现的不同点

## patch
patch -pN < patch_file
patch -R -pN < patch_file
参数：
	-p：后面的N表示取消几层目录的意思
	-R：代表还原，将新的文件还原成原来旧的版本

