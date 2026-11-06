# UEFI+GPT+USB3.0+SSD 安装 Windows 7（X64）

- UEFI+GPT
- USB3.0+SSD

# UEFI+GPT

步骤
- UEFI 引导文件，整合进安装介质
- COMS 设置

注意
- 必须64位系统
- 因为 NTFS 不能进行 UEFI 引导启动 windows 7 安装程序，所以若使用 U 盘，必须要求格式化成 FAT32

## UEFI 引导文件

放置目录
```
X:\efi\boot\bootX64.efi
```

文件来源
- 从一台已经安装了 windows 7 x64 系统的电脑上提取启动文件

      C:\Windows\Boot\EFI\bootmgfw.efi
- 从 windows 7 安装介质中的 install.wim 中提取 bootmgfw.efi
- 从 Windows 8 的安装文件中提取 Bootmgfw.efi 文件

## COMS 设置

- SATA 设置为 AHCI 模式
- CSM 开启
- secure boot 关闭
- 安全启动 设置为 Windows UEFI 模式

# USB3.0+SSD

步骤
- 使用工具将 USB3.0、NVMe 驱动整合进安装介质

## 整合驱动

工具
- 从华硕官网下载 ASUS EZ Installer 系统制作工具

# 问题

- 300 系列主板（除z370外）没有适配 windows 7 的 USB 驱动，所以不用考虑在其上安装
- 200 系列主板，无核显驱动，安装时需要独显