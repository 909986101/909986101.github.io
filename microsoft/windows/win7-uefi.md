# Windows 7 支持 UEFI + GPT

- 实现对 UEFI + GPT 支持

# UEFI + GPT

> 通过提取 `bootmgfw.efi` 文件实现 Windows 7 支持在 UEFI + GPT 环境上安装

步骤
- UEFI 引导文件，整合进安装介质
- COMS 设置

注意（UEFI 的要求）
- 必须 64 位系统
- U 盘必须格式化成  FAT32

## UEFI 引导文件

文件来源（二选一）
- 从一台已经安装了 windows 7 x64 系统的电脑上提取启动文件 `C:\Windows\Boot\EFI\bootmgfw.efi`
- 从 Windows 7 安装介质中的 `install.wim` 中提取 `bootmgfw.efi` 文件

放置位置（改名为 `bootX64.efi`）
```
X:\efi\boot\bootX64.efi
```

## COMS 设置

- SATA 设置为 AHCI 模式
- CSM 开启
- secure boot 关闭
- 启动 设置为 Windows UEFI 模式
