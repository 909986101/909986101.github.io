---
title: 黑苹果声卡驱动
date: 2020-10-02 19:33:54
urlname: Audio-Driver
categories: 黑苹果
tags:
  - AppleALC
---
黑苹果声卡驱动
<!--more-->
# 黑苹果声卡驱动

本文介绍 `AppleALC`。

>An open source kernel extension enabling native macOS HD audio for not officially supported codecs without any filesystem modifications.

## AppleALC

1. github 资源

   https://github.com/acidanthera/AppleALC

1. Installation and usage

   https://github.com/acidanthera/AppleALC/wiki/Installation-and-usage

1. 部署

   1. applealc.kext

      https://github.com/acidanthera/AppleALC/releases

      将 `applealc.kext` 放置在 `/EFI/CLOVER/KEXTS/OTHER/` 目录下。

   1. 查找 `layout-id`，确定 `alcid`

      https://github.com/acidanthera/AppleALC/wiki/Supported-codecs

      以根据声卡 `Codec` 查找到的 `layout-id` 为值，添加 `boot args` 项 `alcid=layout-id`。