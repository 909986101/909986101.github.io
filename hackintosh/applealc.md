# AppleALC

本文介绍 `AppleALC`。

>An open source kernel extension enabling native macOS HD audio for not officially supported codecs without any filesystem modifications.

## github 资源

   https://github.com/acidanthera/AppleALC

## Installation and usage

   https://github.com/acidanthera/AppleALC/wiki/Installation-and-usage

## 部署

1. applealc.kext

https://github.com/acidanthera/AppleALC/releases

将 `applealc.kext` 放置在 `/EFI/CLOVER/KEXTS/OTHER/` 目录下。

2. 查找 `layout-id`，确定 `alcid`

https://github.com/acidanthera/AppleALC/wiki/Supported-codecs

以根据声卡 `Codec` 查找到的 `layout-id` 为值，添加 `boot args` 项 `alcid=layout-id`。