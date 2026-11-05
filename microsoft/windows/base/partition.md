# 安装 Windows 11 时 手动创建分区

**在 Windows 11 26H2 安装界面按 Shift+F10 调出命令提示符，用 diskpart 工具就能手动完成全部分区创建。**

## 步骤

1. 进入命令行环境  

在Windows安装的“现在安装”界面，按下 ‌Shift + F10‌ 组合键，直接调出命令提示符窗口。

2. 启动 diskpart 并确认目标磁盘

```cmd
diskpart
list disk
```

通过容量确认你要安装系统的磁盘编号（通常是 disk 0），后续操作前务必确认，避免误删其他盘数据。

3. 清空磁盘并转换为GPT格式

```cmd
select disk 0
clean
convert gpt
```

clean 会彻底清除该磁盘所有数据，操作前确认已备份重要文件。

4. 按顺序创建4个标准分区

5. 退出工具返回安装界面

关闭命令提示符，回到Windows安装界面点击“刷新”，就能看到刚创建好的分区，直接选中C盘点击下一步即可开始安装。


## 完整示例

```cmd
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
gpt attributes=0x8000000000000001
REM 若不给定大小（size），则会使用当前区域中全部未分配的空间
create partition primary size=204800REM
format quick fs=ntfs label="Windows"
assign letter=C


REM 退出工具返回安装界面
exit
exit
```

这套命令会创建 300MB EFI分区、16MB MSR分区、1GB恢复分区、200GB（或全部未分配的空间） C盘。因为 EFI 分区大于 100MB，解决默认 EFI 空间不足的问题。