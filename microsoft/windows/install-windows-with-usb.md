# 从 USB 闪存驱动器安装 Windows

适用于 Windows 7/8/10/11

## 一、准备 USB 闪存驱动器

1. 创建**主分区**，并设置为**活动分区**
2. 格式化为 **FAT32** 格式

## 二、复制 Windows 安装程序到 USB 闪存驱动器

1. 提取 Windows 产品 DVD 或 ISO 中全部文件至 USB 闪存驱动器

## 三、安装 Windows

略

## 4GB 文件大小限制

当 Windows 映像文件超过 FAT32 4GB 文件大小限制时

将除 Windows 映像文件（sources\install.wim）之外的所有内容复制到 USB 驱动器（拖放或使用此命令，其中 D：是已装载的 ISO，E：是 u 盘）。
```
robocopy D: E: /s /max:3800000000
```

将 Windows 映像文件拆分为较小的文件，并将较小的文件放在 USB 驱动器上：
```
Dism /Split-Image /ImageFile:D:\sources\install.wim /SWMFile:E:\sources\install.swm /FileSize:3800
```

请注意，Windows 安装程序会自动从此文件安装，只要你将其命名为 swm。

## 参考

>https://docs.microsoft.com/zh-cn/windows-hardware/manufacture/desktop/install-windows-from-a-usb-flash-drive