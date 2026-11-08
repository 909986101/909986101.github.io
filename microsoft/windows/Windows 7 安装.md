# UEFI+GPT+USB3.0+SSD 安装 Windows 7（X64）

- UEFI+GPT
- USB3.0+SSD

## UEFI+GPT

步骤
- UEFI 引导文件，整合进安装介质
- COMS 设置

注意
- 必须 64 位系统
- U 盘必须格式化成  FAT32

### UEFI 引导文件

放置目录
```
X:\efi\boot\bootX64.efi
```

文件来源（三选一）
- 从一台已经安装了 windows 7 x64 系统的电脑上提取启动文件 `C:\Windows\Boot\EFI\bootmgfw.efi`
- 从 Windows 7 安装介质中的 `install.wim` 中提取 `bootmgfw.efi` 文件
- 从 Windows 8 的安装文件中提取 `bootmgfw.efi` 文件

### COMS 设置

- SATA 设置为 AHCI 模式
- CSM 开启
- secure boot 关闭
- 安全启动 设置为 Windows UEFI 模式

## USB3.0+SSD

步骤
- 使用工具将 USB3.0、NVMe SSD 驱动整合进安装介质

### 整合驱动

工具
- 从华硕官网下载 `ASUS EZ Installer` 系统制作工具

## 问题

### 300 系列主板

- 仅 H310C 和 B365 有适配 windows 7 的 USB 3.0 驱动。
- 8 代酷睿无核显驱动，安装时需要独显。

### NVMe SSD

- 在 32 位系统上会出现“蓝屏”，建议 64 位系统。

### Legacy + MBR

- USB3.0 和 NVMe SSD 均支持。