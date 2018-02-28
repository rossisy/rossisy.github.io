---
layout: post
title: "System Management Linux"
date: 2018-02-21 20:00:00 +0800
categories: Linux
---
# System Management
## 磁盘与目录的容量查看
df(report file system disk space usage):  
列出文件系统的整体磁盘使用量  
**常用参数:**  
    -a: 列出所有的文件系统，包括系统特有的/proc等文件系统  
    -k: 以KB为单位显示文件系统的容量  
    -m: 以MB为单位显示文件系统的容量  
    -h: 以人们较易阅读的GB、MB、KB等格式自行显示  
    -H：以M=1000K替代M=1024K的进位方式  
    -T：连同该分区的文件系统名称也列出  
    -i：不用硬盘容量，而以inode的数量来显示  

du(estimate file space usage):  
评估文件系统的磁盘使用量  
**常用参数:**  
    -a：列出所有的文件与目录容量，因为默认仅统计目录下面的文件量而已  
    -h：以人们较易读的容量格式（G/M）显示  
    -s：列出总量而已，而不列出每个个别的目录占用容量  
    -S：不包括子目录下的总计  
    -k：以KB列出容量显示  
    -m：以MB列出容量显示  

## 连接文件
Linux下有两种连接文件：hard link和symbolic link
### hard link
若一个inode号对应多个文件名，则这些文件名为硬链接。简单说：hardlink是某个目录下新建一条文件名连接到某inode号码的关联记录而已。

hard link的特性：
* 文件有相同的inode
* 只能对已存在的文件进行创建
* 不能交叉文件系统进行硬链接的创建
* 不能对目录进行创建，只可对文件创建
* 删除一个硬链接文件并不影响其他有相同inode号的文件

### symbolic link
若文件的数据中存放的内容是指向它连接的另一个文件的文件名，则该文件为符号链接。简单说：symbolic link是一个普通的文件，只是数据内容有些特殊，其有自己的inode号及数据块。

symbolic link的特性：
* 软连接有自己的文件属性及权限等
* 可对不存在的文件或目录创建软链接
* 软链接可交叉文件系统
* 软链接可对文件或目录创建
* 创建软链接时，链接计数i_nlink不会增加
* 删除软链接并不影响被指向的文件，但若被指向的原文件被删除，则相关软链接被称为死链接

### 创建链接文件
ln 源文件 目标文件
**常用参数:**
-s：如果不加任何参数就创建链接，那就是hard link，-s就是symbolic link  
-f：如果目标文件存在，主动将目标文件直接删除后再创建  

## 磁盘分区、格式化、检验与挂载
### fdisk（磁盘分区）
fdisk [-l] 设备名称
**参数：**
    -l：输出后面接的设备所有的分区内容。

### mkfs（磁盘分区）
mkfs [-t 文件系统格式] 设备文件名
**参数:**
    -t：可以接文件系统格式，如ext3, ext2, vfat等

### fsck，badblocks（磁盘检验）
fsck [-t 文件系统] [-ACay] 设备名称
**参数：**
    -t：可以接文件系统格式，一般Linux会自动通过super block去分辨文件系统，因此可以不需要这个参数
    -A：依据/etc/fstab的内容，将需要的设备扫描一次。通常开机过程中会执行此命令
    -a：自动修复检查到的有问题的扇区
    -y：与-a类似，但是某些文件系统仅支持-y这个参数
    -C：可以在检验的过程中使用一个直方图来显示目前的进度
    -f：强制检查，一般来说，如果fsck没有发现任何unclean的标志，不会自动进入细化检查，-f可以强制fsck进入细化检查
    -D：针对文件系统下的目录进行优化配置

badblocks -[svw] 设备名称
**参数：**
    -s：在屏幕上列出进度
    -v：可以在屏幕上看到进度
    -w：使用写入的方式来测试，建议不要使用此参数，尤其是待检查的设备已有文件时

## 磁盘挂载与卸载
### mount（挂载）
mount -[altLon] 设备文件名 挂载点
**参数：**
    -a：依照配置文件/etc/fstab的数据将所有未挂载的磁盘都挂载上来
    -l：单纯输入mount会显示目前挂载的信息，加上-l可增列Label名称
    -t：与mkfs的参数非常类似的，可以加上文件系统种类来指定与挂载的类型
    -n：在默认的情况下，系统会将实际挂载的情况实时写人/etc/mtab中，以利其他程序的运行。但在某些情况下为了避免问题，会刻意不写人，此时就得要使用这个-n的参数
    -L：系统除了利用设备文件名之外，还可以利用文件系统的卷标名称（Label）来进行挂载。
    -o：后面可以接一些挂载时额外加上的参数，如账号、密码、读写权限等。ro（挂载文件系统成为只读），rw（挂载文件系统成为可读写），aync（同步写人系统的内存机制），async（异步写人系统的内存机制），auto（允许此分区被以mount -a自动挂载，noauto（不允许自动挂载），dev（允许此分区上可以创建设备文件），nodev（不允许创建设备文件），suid/nosuid（是否允许此分区含有suid/sgid的文件格式，exec/noexec（是否允许此分区上拥有可执行binary文件），user/nouser（是否允许此分区让任何用户执行mount），默认值为rw，suid，dev，exec，auto，nouser，async，remount（重新挂载）

### umount（卸载）
umount [-fn] 设备文件名或挂载点
**参数：**
    -f：强制卸载。可用在类似网络文件系统（NFS）无法读取的情况下
    -n：不更新/etc/mtab的情况下卸载

## 磁盘参数修改
mknod（make block or character special files）
mknod 设备文件名 [bcp] [Major] [Minor]
**参数：**
    b：设置设备名称为一个外部存储设备文件，如硬盘
    c：设置设备名称为一个外部输入设备文件，如鼠标/箭牌
    p：设置设备名称为一个FIFO文件
    Major：主设备代码
    Minor：次设备代码

e2label (Change the label on an ext2/ext3/ext4 filesystem）
e2label 设备名称 新的Label名称

tune2fs（adjust tunable filesystem parameters on ext2/ext3/ext4 filesystems）
tune2fs [-jlL] 设备代号
**参数：**
    -l：类似dumpe2fs -h的功能。将super block内的数据读出来
    -j：将ext2的文件系统转换为ext3的文件系统
    -L：类似e2label的功能，可以修改文件系统的Label

## 开机挂载
### /etc/fstab及/etc/mtab
/etc/fstab（file system table）就是将我们利用mount命令进行挂载时，将所有的参数写入到这个文件就可以了。除此之外，/etc/fstab还添加了dump这个备份用的命令支持，与开机时是否进行文件系统检验fsck等命令有关。  
这个文件的内容有六个字段：
1. 磁盘设备文件名或该设备的Label：这个字段填入文件系统的设备文件名
2. 挂摘点（mount point）：一定是目录
3. 磁盘分区的文件系统：文件系统，如ext2，ext3，ext4
4. 文件系统参数：mount命令中的特殊文件系统参数
5. 能否被dump备份命令作用：0代表不要做dump备份，1代表要每天进行dump操作，2页代表其他不定日期的dump备份操作
6. 是否已fsck检验扇区：0代表不要检验，1表示最早检验（一般只有根目录会设置为1），2也是要检验。开机过程中，系统默认会以fsck检验我们的文件系统是否完整（clean），不过某些文件系统是不需要检验的，例如内存交换空间（swap）或特殊文件系统
/proc与/sys等。

/etc/mtab与/proc/mounts这两个文件记录了实现文件系统的挂载，每次我们在改动文件系统的挂载时，也会同时改动这两个文件。

## 特殊设备loop挂载（镜像文件不刻录就挂载使用）
一般的光盘镜像文件都是刻录成光盘后才能够使用该文件内的数据的，在windows系统下我们也可以使用虚拟机来载入镜像文件以读取文件内容，而在Linux下我们通过loop设备来挂载镜像文件以读取文件内容。如：
```
mount -o loop 镜像文件 挂载目录
```

## 内存交换空间（swap）的构建
Linux系统安装时，若没有设置swap，手动创建swap的方法。
1. 使用物理分区构建swap
    Step1：分区。使用fdisk在磁盘中分出一个分区给系统作为swap，并修改该分区的系统ID为swap，并使用partprobe命令让内核更新分区表
    Step2：格式化。使用命令mkswap格式化swap分区
    Step3：使用。用命令swapon启动该swap设备
    Step4：查看。通过free命令查看内存的使用情况

2. 使用文件构建swap
    Step1：新建文件。使用dd命令在/tmp下新建个指定大小的文件
    Step2：格式化。使用命令mkswap格式化该文件为swap的文件格式
    Step3：使用。用命令swapon启动该swap设备
    Step4：查看。通过free命令查看内存的使用情况

## parted（分区）
支持2TB以上的分区操作
parted [设备] [命令] [参数]
命令：
    1. mkpart（新增分区）
       mkpart [primary|logical|extended] [ext3|vfat] 开始 结束
    2. print（显示分区表）
    3. rm（删除分区）
       rm [partition]
