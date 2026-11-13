# Windows 7 x64 最小化补丁

|KB|类型|描述|更新时间|
|:--|:--|:--|:--|
|KB3020369|SSU|KB3125574 的专用前置 SSU|2015.05.12|
|KB4490628|SSU|服务堆栈更新（SSU）|2019.03.12|
|KB4474419|安全更新|SHA-2 代码签名支持|2019.09.10|
|KB3125574|更新程序|面向 Win7 SP1 的“便捷汇总”，包含了 SP1 发布后到 2016 年 4 月所有非安全更新|2016.05.17|
|KB3140245|更新程序|TLS 1.2 功能|2016.06.14|
|KB3172605|更新程序|后续 TLS 协议的可靠性修复补丁|2016.09.13|
|KB4534310|安全更新|Windows 7 官方免费通道的最后一个月度安全质量汇总，2020 年 1 月|2020.01.14|

```text
KB3020369
KB4490628
KB4474419
KB3125574
KB3140245
KB3172605
KB4534310
```

# 集成补丁

## 目录及文件准备

详见：[使用 DISM 为 Windows 7 注入 USB3.0 和 NVMe 驱动](./win7-injection-usb3-nvme.md)

## install.wim 加入补丁

```powershell
dism /Mount-WIM /WimFile:D:\mkos\os\sources\install.wim /Index:1 /MountDir:D:\mkos\mount

dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\windows6.1-kb3020369-x64_5393066469758e619f21731fc31ff2d109595445.msu
dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\windows6.1-kb4490628-x64_d3de52d6987f7c8bdc2c015dca69eac96047c76e.msu
dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\windows6.1-kb4474419-v3-x64_b5614c6cea5cb4e198717789633dca16308ef79c.msu
dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\windows6.1-kb3125574-v4-x64_2dafb1d203c8964239af3048b5dd4b1264cd93b9.msu
dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\windows6.1-kb3140245-x64_5b067ffb69a94a6e5f9da89ce88c658e52a0dec0.msu
dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\windows6.1-kb3172605-x64_2bb9bc55f347eee34b1454b50c436eb6fd9301fc.msu
dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\windows6.1-kb4534310-x64_4dc78a6eeb14e2eac1ede7381f4a93658c8e2cdc.msu

dism /UnMount-Wim /MountDir:D:\mkos\mount /Commit
```

## 给 install.wim 瘦身

详见：[使用 DISM 为 Windows 7 注入 USB3.0 和 NVMe 驱动](./win7-injection-usb3-nvme.md)