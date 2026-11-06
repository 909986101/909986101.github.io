---
title: 使用diskpart命令
date: 2020-09-14 22:10:52
urlname: use-diskpart
categories: windows
tags: 
  - windows
  - diskpart
---
使用 diskpart 命令
<!--more-->
# 使用 diskpart 命令

diskpart 命令是 Windows 下的磁盘工具。Windows 系统、PE、Windows 安装盘中的命令行（其实就是 PE）都可以调用该命令。

## 基础

1. 启动

   命令行中输入 `diskpart` 并回车，即可进入 `diskpart` 命令交换界面。
   
   ```
   PS C:\windows\system32> diskpart

   Microsoft DiskPart 版本 10.0.19041.1

   Copyright (C) Microsoft Corporation.
   在计算机上: li-PC

   DISKPART>
   ```

1. 帮助

   在 `diskpart` 交换界面输入 `help` 即可获得子命令。

    ```
    DISKPART> help

    Microsoft DiskPart 版本 10.0.19041.1

    ACTIVE      - 将选中的分区标记为活动的分区。
    ADD         - 将镜像添加到一个简单卷。
    ASSIGN      - 给所选卷分配一个驱动器号或装载点。
    ATTRIBUTES  - 操纵卷或磁盘属性。
    ATTACH      - 连接虚拟磁盘文件。
    AUTOMOUNT   - 启用和禁用基本卷的自动装载。
    BREAK       - 中断镜像集。
    CLEAN       - 从磁盘清除配置信息或所有信息。
    COMPACT     - 尝试减少文件的物理大小。
    CONVERT     - 在不同的磁盘格式之间转换。
    CREATE      - 创建卷、分区或虚拟磁盘。
    DELETE      - 删除对象。
    DETAIL      - 提供对象详细信息。
    DETACH      - 分离虚拟磁盘文件。
    EXIT        - 退出 DiskPart。
    EXTEND      - 扩展卷。
    EXPAND      - 扩展虚拟磁盘上可用的最大大小。
    FILESYSTEMS - 显示卷上当前和支持的文件系统
    FORMAT      - 格式化卷或分区
    GPT         - 给选择的 GPT 分区分配属性。
    HELP        - 显示命令列表。
    IMPORT      - 导入磁盘组。
    INACTIVE    - 将所选分区标为不活动。
    LIST        - 显示对象列表。
    MERGE       - 将子磁盘与其父磁盘合并。
    ONLINE      - 使当前标为脱机的对象联机。
    OFFLINE     - 使当前标记为联机的对象脱机。
    RECOVER     - 刷新所选包中所有磁盘的状态。
                尝试恢复无效包中的磁盘，并
                重新同步具有过时丛或奇偶校验数据
                的镜像卷和 RAID5 卷。
    REM         - 不起任何作用。用来注释脚本。
    REMOVE      - 删除驱动器号或装载点分配。
    REPAIR      - 用失败的成员修复一个 RAID-5 卷。
    RESCAN      - 重新扫描计算机，查找磁盘和卷。
    RETAIN      - 在一个简单卷下放置一个保留分区。
    SAN         - 显示或设置当前启动的操作系统的 SAN 策略。
    SELECT      - 将焦点移动到对象。
    SETID       - 更改分区类型。
    SHRINK      - 减小选定卷。
    UNIQUEID    - 显示或设置磁盘的 GUID 分区表(GPT)标识符或
                主启动记录(MBR)签名。

    DISKPART>
    ```

1. 帮助子命令

   以子命令 `select` 为例。

    ```
    DISKPART> help select

    Microsoft DiskPart 版本 10.0.19041.1

    DISK        - 将焦点移动到磁盘。例如，SELECT DISK。
    PARTITION   - 将焦点移动到分区。例如，SELECT PARTITION。
    VOLUME      - 将焦点移动到卷。例如，SELECT VOLUME。
    VDISK       - 将焦点转移到虚拟磁盘。例如，SELECT VDISK。
    ```

   发现有 4 个选项，这里以 `disk` 为例。

    ```
    DISKPART> help select disk

        选择指定的磁盘并将焦点切换到该磁盘。

    语法:  SELECT DISK=<N>
            SELECT DISK=SYSTEM
            SELECT DISK=NEXT
            SELECT DISK=<Path>

        DISK=<N>
                    要接收焦点的磁盘
                    的 DiskPart 磁盘索引号。

        DISK=<Path>
                    要接收焦点的磁盘的位置路径。

        DISK=SYSTEM
                    在 BIOS 计算机上，BIOS 磁盘 0 将接收焦点。
                    在 EFI 计算机上，用于当前启动的
                    包含 ESP 分区的磁盘将接收焦点。在 EFI
                    计算机上，如果没有 ESP，或者存在多个
                    ESP，或者计算机从 Windows PE 启动，
                    该命令都将失败。

        DISK=NEXT
                    选择磁盘后，将对磁盘列表中的所有磁盘循环执行
                    此命令。列表中的下一个磁盘
                    将接收焦点。如果下一个磁盘是
                    枚举的开始位置，则此命令将失败，任何磁盘都将没有
                    焦点。


        如果未指定选项，则 select 命令将列出当前带有焦点的
        磁盘。你可以使用 LIST DISK 命令查看计算机上所有磁盘的
        DiskPart 索引号。

    示例:

        SELECT DISK=1
        SELECT DISK=SYSTEM
        SELECT DISK=NEXT
        SELECT DISK=PCIROOT(0)#PCI(0100)#ATA(C00T00L01)

    DISKPART>
    ```
   
   至此我们获得了 `select disk` 的用法。

   其他命令以此类推。

## 常用命令

1. 显示列表（list）、移动焦点（select）

   先看一下所有的磁盘

    ```
    DISKPART> list disk

     磁盘 ###  状态           大小     可用     Dyn  Gpt
     --------  -------------  -------  -------  ---  ---
     磁盘 0    联机              476 GB      0 B        *
     磁盘 1    联机              465 GB  1024 KB        *
     磁盘 2    联机              465 GB  1024 KB
    ```

   焦点移动到 disk 0 上，注意那个星号（*）

    ```
    DISKPART> select disk 0

    磁盘 0 现在是所选磁盘。

    DISKPART> list disk

      磁盘 ###  状态           大小     可用     Dyn  Gpt
      --------  -------------  -------  -------  ---  ---
    * 磁盘 0    联机              476 GB      0 B        *
      磁盘 1    联机              465 GB  1024 KB        *
      磁盘 2    联机              465 GB  1024 KB
    ```

   显示 disk 0 上的 分区

    ```
    DISKPART> list part

      分区 ###       类型              大小     偏移量
      -------------  ----------------  -------  -------
      分区      1    系统                 100 MB  1024 KB
      分区      2    系统                 200 MB   101 MB
      分区      3    主要                 326 GB   301 MB
      分区      4    未知                 150 GB   326 GB
    ```

   焦点移动到 partition 1 上面，注意那个星号（*）

    ```
    DISKPART> select part 1

    分区 1 现在是所选分区。

    DISKPART> list part

      分区 ###       类型              大小     偏移量
      -------------  ----------------  -------  -------
    * 分区      1    系统                 100 MB  1024 KB
      分区      2    系统                 200 MB   101 MB
      分区      3    主要                 326 GB   301 MB
      分区      4    未知                 150 GB   326 GB
    ```

   显示 volume

    ```
    DISKPART> list vol

      卷 ###      LTR  标签         FS     类型        大小     状态       信息
      ----------  ---  -----------  -----  ----------  -------  ---------  --------
      卷     0     C   W10P         NTFS   磁盘分区         326 GB  正常         启动
      卷     1                      FAT32  磁盘分区         100 MB  正常         系统
      卷     2         EFI 2        FAT32  磁盘分区         200 MB  正常         已隐藏
      卷     3     E   Win10_old    NTFS   磁盘分区         465 GB  正常
      卷     4         EFI          FAT    磁盘分区         629 MB  正常         已隐藏
      卷     5     F   Seagate Sli  NTFS   磁盘分区         465 GB  正常
    ```

1. set

   作用：指定新分区类型。

   |类型|值|说明|
   |:-|:-|:-|
   |EFI 系统分区|`c12a7328-f81f-11d2-ba4b-00a0c93ec93b`|设置为 ESP 分区|
   |基本数据分区|`ebd0a0a2-b9e5-4433-87c0-68b6b72699c7`|顾名思义，分配盘符就可以在在资源管理器中访问了|
   
   示例：设置 disk 0 的 partition 1 为基本数据分区

   ```
   DISKPART> select disk 0

   磁盘 0 现在是所选磁盘。

   DISKPART> select part 1

   分区 1 现在是所选分区。

   DISKPART> set id=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7
   ```

1. assign

   作用：为带焦点的卷分配一个驱动器号或已安装文件夹路径名称。

   > 你无法为启动卷或含有页面文件的卷分配驱动器号。  
   此外，你也无法为原始设备制造商(OEM)分区(除非启动到 Windows PE)或除基本数据分区以外的任何 GUID 分区表(GPT)分区、ESP 分区或恢复分区分配驱动器号。

   > 必须选择一个卷才能成功执行此操作。

   示例：给 volume 2 分配盘符 D

   ```
   DISKPART> select vol 2

   卷 2 是所选卷。

   DISKPART> ASSIGN LETTER=D
   ```

1. remove

   作用：移除盘符

   assign 命令可以给一个卷分配盘符，那么可以用 remove 命令把盘符移除。

   示例：将 volume 2 盘符 D 移除

   ```
   DISKPART> select vol 2

   卷 2 是所选卷。

   DISKPART> remove LETTER=D
   ```