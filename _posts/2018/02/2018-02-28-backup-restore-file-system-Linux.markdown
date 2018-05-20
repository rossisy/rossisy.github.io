---
layout: post
title: "Backup and Restore File System in Linux"
date: 2018-02-28 22:00:00 +0800
categories: Linux
---
# Backup and Restore
## dump
dump命令用于ext2/3/4文件系统的备份，支持整个文件系统或是单一目录的备份。  
若只用于备份目录而非单一文件系统时，此命令会有所限制：备份数据必须要在备份目录下；仅能使用level0即完整备份；不支持-u参数即无法创建/etc/dumpdates这个level备份的时间记录文件  

dump [-Suvj] [-level] [-f 备份文件] 待备份数据  

**参数：**  
    -S：仅列出后面的待备份数据需要多少磁盘空间才能够备份完毕  
    -u：将这次dump的时间记录到/etc/dumpdates文件中  
    -v：将dump的文件过程显示出来  
    -j：加入bzip2的支持，将数据进行压缩，默认bzip2压缩等级为2  
    -level：从0~9共10个等级，0表示完成备份，大于0的都是增量备份，指定dump备份从上次低一级备份后有更新的文件  
    -f：后面接文件，将backup写入该文件，可接设备文件如/dev/st0等  
    -W：列出在/etc/fstab里面的具有dump设置的分区是否有备份过  

## restore
restore用于恢复备份的文件系统  

restore -t [-f dumpfile] [-h]  
用来查看dump文件  

restore -C [-f dumpfile] [-D 挂载点]  
比较dump与实际文件  

restore -i [-f dumpfile]  
进入互动模式  

restore -r 【-f dumpfile]  
还原整个文件系统  

**参数：**  
    -t：此模式用在查看dump起来的备份文件中含有什么重要数据。类似tar -t功能。  
    -C：此模式可以将dump内的数据拿出来跟实际的文件系统做比较，最终会列出“在dump文件内有记录的且目前文件系统不一样”的文件  
    -i：进入互动模式，可以仅还原部分文件，用在dump目录时的还原  
    -r：将整个文件系统还原的一种模式，用在还原针对文件系统的dump备份  
    -h：查看完整备份数据中的inode与文件系统label等信息  
    -f：后面就接你要处理的那个dump文件  
    -D：与-C进行搭配，可以查出后面接的挂载点与dump内有不同的文件  

## dd
转变、拷贝文件

dd if="input_file" of="output_file" bs="block_size" count="number"

**参数：**  
    if：就是input file，也可以是设备  
    of：就是output file，也可以是设备  
    bs：规划的一个block的大小，若未指定则默认是512bytes（一个扇区的大小）  
    count：多少个bs的意思  

## cpio
拷贝文件至存档中或从存档中拷贝文件  

cpio -ovcB > [file|device]  
备份  

cpio -ivcdu < [file|device]  
还原  

cpio -ivct < [file|device]  
查看  

**参数：**  
    -o：将数据copy输出到文件或设备上
    -B：让默认的blocks可以增加至5120 bytes，默认是512 bytes
    -i：将数据自文件或设备复制到系统当中
    -d：自动新建目录
    -u：自动将较新的文件覆盖较旧的文件
    -t：需配合-i参数，可用在查看以cpio新建的文件或设备的内容
    -v：让存储的过程中文件名可以在屏幕上显示
    -c：一种较新的portable format方式存储

