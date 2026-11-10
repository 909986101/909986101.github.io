# 安装 Windows 11 时 手动创建分区

> 在 Windows 11 26H2 安装界面按 Shift+F10 调出命令提示符，用 diskpart 工具就能手动完成全部分区创建。

## 步骤

### 进入命令行环境  

在 Windows 安装的“现在安装”界面，按下 ‌Shift + F10‌ 组合键，直接调出命令提示符窗口。

### 启动 diskpart 并确认目标磁盘

```cmd
diskpart
list disk
```

通过容量确认你要安装系统的磁盘编号（通常是 **disk 0**），后续操作前务必确认，避免误删其他盘数据。

### 清空磁盘并转换为GPT格式

```cmd
select disk 0
clean
convert gpt
```
> [!Caution]
> **clean** 会彻底清除该磁盘所有数据，操作前确认已备份重要文件。

### 按顺序创建 4 个标准分区

### 退出工具返回安装界面

关闭命令提示符，回到 Windows 安装界面点击“刷新”，就能看到刚创建好的分区，直接选中 C 盘点击下一步即可开始安装。

## 完整示例

这套命令会创建

|分区|大小|SETID|
|:--|--:|--:|
|EFI|300MB|`c12a7328-f81f-11d2-ba4b-00a0c93ec93b`|
|MSR|16MB|`e3c9e316-0b5c-4db8-817d-f92df00215ae`|
|Recovery|1GB|`de94bba4-06d1-4d40-a16a-bfd50179d6ac`|
|C|200GB <br>或全部未分配的空间|`ebd0a0a2-b9e5-4433-87c0-68b6b72699c7`|

因为 EFI 分区大于 100MB，解决默认 EFI 空间不足的问题。

```batch
REM 进入命令行
REM 启动 diskpart 并确认目标磁盘
diskpart
list disk


REM 清空磁盘并转换为GPT格式
select disk 0
clean
convert gpt


REM 创建分区（EFI、MSR、Recovery、Windows）
create partition efi size=300
format quick fs=fat32 label="System"
create partition msr size=16
create partition primary size=1024
format quick fs=ntfs label="Recovery"
set id="de94bba4-06d1-4d40-a16a-bfd50179d6ac"
REM 设置属性默认隐藏（不分配盘符）
gpt attributes=0x8000000000000001
REM 若不给定大小（size），则会使用当前区域中全部未分配的空间
create partition primary size=204800
format quick fs=ntfs label="Windows"
assign letter=C


REM 退出工具返回安装界面
exit
exit
```
