---
layout: post
title: "Directory tree in Linux"
date: 2018-01-30 22:00:00 +0800
categories: Linux
---
# 目录树结构
目录树结构（directory tree）是以根目录(/)为主，然后向下呈现分支状的目录结构的一种文件结构。  
CentOS7系统目录树结构如下：  
/  
|\_bin -> usr/bin  
|\_sbin -> usr/sbin  
|\_lib64 -> usr/lib64  
|\_lib -> usr/lib  
|\_/etc  
|\_/dev  
|\_/proc  
|\_/var  
|\_/usr  
|\_/home  
|\_/boot  
|\_/opt  
|\_/mnt  
|\_/media  
|\_/srv  
|\_/root  
|\_/sys  
|\_/run  
|\_/tmp  

**/**  
  根目录(root directory), Linux中只有一个根目录，所有的数据都存放在这个目录下。

**bin**  
  标准Linux工具目录(User binaries)，此目录下存放的是供所有Linux用户使用的标准Linux工具。

**sbin**  
  系统工具目录(System binaries), 此目录下存放的是供root用户使用的系统工具。

**lib64**  
  64位系统库目录(Library64), 此目录下存放的是64位的系统库文件。

**lib**  
  系统库目录(Library), 此目录下存放的是32位的系统库文件。  

**/etc**  
  系统配置文件目录, 此目录下存放的是系统的配置文件。  

**/dev**  
  系统设备目录(Device), 此目录下存放的是与设备有关的文件。

**/proc**  
  proc文件系统的挂载目录(process information), 此目录存放操作系统运行时的进程信息及内核信息。

**/var**  
  频繁变动的文件目录(Vary), 此目录用于存放系统执行过程中经常修改的文件,例如：系统日志文件的存放目录/var/log。

**/usr**  
  用户的额外工具目录(User Programs), 此目录用于存放不适于放在bin或sbin目录下的工具。

**/home**  
  用户数据的存放目录, 此目录用于存放除root用户以外其他用户的数据。每个用户在/home目录下都有自己的用户目录/home/用户名，用于存放其用户数据。

**/boot**  
  系统启动的相关文件目录，此目录用于存放Linux内核及引导系统程序所需要的文件。

**/opt**  
  可选择的文件目录，此目录用于存放自定义的工具。某些工具或软件默认的安装目录就是/opt。

**/mnt**  
  设备临时挂载目录，此目录用于存放挂载设备的挂载目录。

**/media**  
  媒介目录，有些Linux的发行版会将USB接口的移动硬盘挂载到此目录下。

**/srv**  
  服务数据目录，此目录用于存放服务启动后需要访问的数据。

**/root**  
  系统管理员的home目录，此目录用于存放root的用户数据。

**/sys**  
  系统文件目录，此目录用于存放系统内核相关的文件。

**/run**  
  运行时文件目录，此目录用于存放进程运行时产生的一些临时文件。

**/tmp**  
  系统临时文件目录，此目录用于存放临时文件。
