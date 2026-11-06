---
title: 黑苹果UDH630核显HDMI输出黑屏解决的一点体会
date: 2020-09-01 08:11:50
urlname: hackintosh-uhd630-hdmi-black-screen
categories: 黑苹果
tags: 黑苹果
---
黑苹果 UDH630 核显 HDMI 输出黑屏解决的一点体会
<!--more-->
# 黑苹果 UDH630 核显 HDMI 输出黑屏解决的一点体会

硬件配置
- 华硕 B365M-KYLIN
- I3 9100（核显 UHD630）
- 无独显

大致步骤
1. 确定 `ig-platform-id`
1. 修改接口类型为 `HDMI`
1. 禁用 `AGDC`

## 准备工作

请仔细阅读下面链接中“**建议**”一段的内容，并对照自己的 `Clover` 或 `OC` 配置进行更改。

>| https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.cn.md

## 确定 `ig-platform-id`

1. 核显型号

   首先要知道核显是什么型号，intel 官网可以查到

   > https://ark.intel.com

   查询得知我的 CPU 是 I3 9100，核显为 UHD630

1. `ig-platform-id`

   接下来根据核显型号查询合适的 `ig-platform-id`，请详细阅读下面链接中 “UHD 610-655（Coffee Lake 微架构，下文简称 CFL）”一段的内容

   > https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.cn.md

   因为是台式机，推荐使用 `0x3E9B0007`

   > 推荐的 FB 设置：0x3EA50000（桌面版，缺省值）或 0x3E9B0007（桌面版，推荐）；0x3EA50009（移动版，缺省值）。

## 修改接口类型为 `HDMI`

`ig-platform-id` 确定了，要修改接口类型为 `HDMI`，继续查表，请详细查看下面链接中“CFL 平台详细信息（点击此处以展开）”一段的内容，

> https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.cn.md

注意最后三行中的 `00040000`，代表接口类型为 `DP`，修改为 `00080000` 就是 `HDMI` 类型了。

```
ID: 0x3E9B0007, STOLEN: 57 MB, FBMEM: 0 bytes, VRAM: 1536 MB, Flags: 0x00801302
TOTAL STOLEN: 58 MB, TOTAL CURSOR: 1 MB (1572864 bytes), MAX STOLEN: 172 MB, MAX OVERALL: 173 MB (181940224 bytes)
Model name: Intel UHD Graphics 630
Camelia: CameliaDisabled (0), Freq: 0 Hz, FreqMax: 0 Hz
Mobile: 0, PipeCount: 3, PortCount: 3, FBMemoryCount: 3
[1] busId: 0x05, pipe: 9, type: 0x00000400, flags: 0x000003C7 - ConnectorDP
[2] busId: 0x04, pipe: 10, type: 0x00000400, flags: 0x000003C7 - ConnectorDP
[3] busId: 0x06, pipe: 8, type: 0x00000400, flags: 0x000003C7 - ConnectorDP
01050900 00040000 C7030000
02040A00 00040000 C7030000
03060800 00040000 C7030000
```

## ~~禁用 `AGDC`~~

~~系统为 10.15.6 使用核显 UHD630 用于显示时，可能在启动到登陆界面时会黑屏。解决办法是“禁用 AGDC”。~~

~~二选一~~
- ~~启动参数：`igfxagdc=0`~~
- ~~config.plist 文件中 `Devices`，`Propertise` 添加 `disable-agdc`，属性值为 `01000000`。~~

## 启用 `igfxonln=1`

>In macOS 10.15.4, there were some changes made to AGPM that can cause wake issues on Coffee Lake systems. Specifically displays hooked up to the iGPU would fail to wake. To resolve this:

- Add igfxonln=1 to boot-args
- Make sure you're using WhateverGreen v1.3.8 or newer

## 配置总结

根据以上所述，下表是配置总结

|属性键|属性值|值类型|描述|
|:-|:-|:-|:-|
|`ig-platform-id`|`07009B3E`|`DATA`||
|`framebuffer-patch-enable`|`01000000`|`DATA`|帧缓冲总开关|
|~~`disable-agdc`~~|~~`01000000`~~|~~`DATA`~~||
|`framebuffer-con0-enable`|`01000000`|`DATA`||
|`framebuffer-con0-alldata`|`01050900 00080000 C7030000`|`DATA`||
|`framebuffer-con0-enable`|`01000000`|`DATA`||
|`framebuffer-con0-alldata`|`02040A00 00080000 C7030000`|`DATA`||
|`framebuffer-con0-enable`|`01000000`|`DATA`||
|`framebuffer-con0-alldata`|`03060800 00080000 C7030000`|`DATA`||