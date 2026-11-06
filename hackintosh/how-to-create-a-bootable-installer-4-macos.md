---
title: 黑苹果制作U盘安装盘
date: 2020-09-15 19:52:41
urlname: how-to-create-a-bootable-installer-4-macos
categories:
tags:
---
黑苹果制作 MacOS U 盘安装盘
<!--more-->
# 黑苹果制作 MacOS U 盘安装盘

## 白果的安装盘制作

> 参考：如何创建可引导的 macOS 安装器  
https://support.apple.com/zh-cn/HT201372

以 Catalina 为例

1. 下载 macOS

   安装器会以名为“Install macOS Catalina”的 App 的形式直接下载到您的“应用程序”文件夹。

1. 在“终端”中使用“createinstallmedia”命令

   U 盘
   - 宗卷至少有 12GB 可用储存空间
   - 并已格式化为 Mac OS 扩展格式

   ```
   sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
   ```

为什么要讲白果的 U 盘安装盘呢？

- 苹果 macOS 操作系统只能安装在苹果电脑上。如果仿冒环境让安装程序认为是苹果电脑，就可以进行安装了。这由 `OC` 或 `CLOVER` 来实现。
- 黑果和白果的安装盘区别就是黑果的多了一个 `ESP` 分区，里面放着 `OC` 或者 `CLOVER`。

## 黑果的安装盘制作

有了白果的制作经验，黑果就简单了。只需要创建一个 `ESP` 分区，把 `OC` 或 `CLOVER` 复制进去即可。

## 将 dmg 文件灌入 U 盘

很多大佬，比如黑果小兵，会提供 dmg 镜像。这种镜像里面包含了 `ESP` 分区和 `Install macOS Catalina` 分区。只需要用工具将 dmg 镜像灌入 U 盘即可。

- Windows

  使用 `etcher` 软件

- Linux
 
  `dd` 命令，so easy

- mac OS

  “磁盘工具”是个好工具