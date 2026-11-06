---
title: 黑苹果Clover简介
date: 2020-09-21 14:36:10
urlname: clover-introduce
categories: 黑苹果
tags: clover
---
黑苹果 Clover 简介
<!--more-->
# 黑苹果 Clover 简介

本文只是对 Clover 简单的介绍。

## Clover 是什么

Clover（四叶草），是的没错它就是“植物大战僵尸”中的“三叶草”加了一个叶子。

Clover 是一款黑苹果系统引导工具。提供硬件环境仿冒、内核扩展（驱动程序）支持等等。

## Clover 目录结构

1. `config.plist` 配置文件

   这个是必须的。里面有 Clover 对于 MacOS 系统的配置。

1. `kexts` 目录

   这个目录放置了内核扩展（kernel extension），就是设备驱动程序。有 2 个目录可以关心一下。

   1. `other` 所有需要加载的 kext，都需要放在这个目录下。

   1. `off` 顾名思义，放在里面的 kext 都不会被加载。

1. `drivers` 目录

   又是“驱动”，可以这样认为，这里放置的是 `Clover` 自己用的“驱动”。

   1. `UEFI` 目录，如果你使用 `uefi` 方式引导计算机，那么就把 `.efi` 文件放置在此。

1. `themes` 目录

   放置的都是“主题”

1. `tools` 目录

   放置了一些工具（`.efi`），个人觉得有用的是 `UEFI Shell`。

1. `CLOVERX64.efi` 文件

   这个就是 Clover 的 bootloader。替换这个文件就是更新 Clover。

## 资源

1. github

   链接：https://github.com/CloverHackyColor/CloverBootloader/releases

   |文件|描述|
   |:-|:-|
   |`CloverV2-XXXX.zip` |完整的 Clover，解开就是 `Clover`，还包括 `boot` 目录。|
   | `CLOVERX64.efi.zip` |Clover 的 bootloader。|
   | `Clover_rXXXX.pkg` |Clover 的安装包（macOS 下），可以自定义安装 Clover。|