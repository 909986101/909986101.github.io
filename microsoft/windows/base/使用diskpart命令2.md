---
title: 使用diskpart命令2
date: 2020-09-15 08:40:01
urlname: use-diskpart-2
categories: windows
tags:
  - windows
  - diskpart
---
使用 diskpart 命令 2
<!--more-->
# 使用 diskpart 命令 2

diskpart 命令是 Windows 下的磁盘工具。Windows 系统、PE、Windows 安装盘中的命令行（其实就是 PE）都可以调用该命令。

## 进（危）阶（险）命令

1. clean

   Removes any and all partition or volume formatting from the disk with focus.

   把整个盘清掉，刺不刺激

   示例：disk 0 清盘

   ```
   DISKPART> select disk 0

   Disk 0 is now the selected disk.

   DISKPART> clean
   ```

1. CONVERT GPT

   Convert a disk from MBR to GPT.

   没什么好讲的。

1. CREATE

   创建对象（分区、卷或者虚拟磁盘）

   示例：创建一个 200MB 的 ESP 分区

   ```
   DISKPART> select disk 0
   DISKPART> create part efi size=200
   ```


1. DELETE

   Delete an object.

   有创建就会有删除，先移动焦点到对象，再删除。

   ```
   DISKPART> select disk 0

   Disk 0 is now the selected disk.

   DISKPART> select partition 1

   Partition 1 is now the selected partition.

   DISKPART> delete
   ```

1. FORMAT

   Formats the specified volume for use with Windows.

   示例：格式化 disk 0 的 partition 1，文件格式为 FAT32、卷标为 EFI，使用快速格式化。
   
   ```
   format fs=fat32 label="EFI" quick
   ```

## 实战

1. 需求：将 disk 2 转换为 GPT，创建 2 个 ESP 分区并格式化为 FAT32 格式。

   ```
   list disk
   select disk 2
   convert gpt
   create partition efi size=100
   create partition efi size=200
   select part 1
   format fs=fat32 label="EFI-1" quick
   select part 2
   format fs=fat32 label="EFI-2" quick
   ```

1. 需求2：将上面的 partition 1 设置为“基本数据分区”，并分配盘符“S”

   ```
   select disk 2
   select partition 1
   set id=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7
   assign letter=s
   ```