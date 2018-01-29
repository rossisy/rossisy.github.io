---
layout: post
titil: "Partition file in Linux"
date: 2018-01-29 22:06:00 +0800
categories: Linux
---
# 硬盘分区表
分区表（partition table）是记录整块硬盘分区状态的一块大小为64bytes的区域。分区表总共为四组记录区，每组记录区记录了该区段的起始与结束位置。

# 硬盘分区在Linux中的设备文件名
若硬盘的设备文件名为/dev/hda且创建了4个分区，则这4个分区在Linux中的设备文件名为：
  P1: /dev/hda1
  P2: /dev/hda2
  P3: /dev/hda3
  P4: /dev/hda4
分区表中指定的四个分区被称为主（Primary）分区或扩展（Extended）分区。若为扩展分区则可以使用额外的扇区来记录分区信息，由扩展分区切出来的分区称为逻辑分区（logical partition）。因hda1~hda4是保留给主分区或扩展分区用的，所以逻辑分区的设备文件名则是从hda5开始。
