---
title: 黑苹果显卡驱动
date: 2020-09-24 09:14:13
urlname: display-driver
categories: 黑苹果
tags: 
  - 核显
  - nvidia
  - amd
---
黑苹果显卡驱动
<!--more-->
# 黑苹果显卡驱动

|显卡分类||
|:-|:-|
|厂商|Intel 核显、Nvidia、AMD|
|能否驱动|免驱、需要驱动、无解|

虽然说是“免驱”，但还是需要 `Lilu` 和 `WhateverGreen` 的。

## Intel 核显

1. 确定核显型号

   访问 ark.intel.com，根据 CPU 型号，可查到核显型号。

1. 确定 `ig-platform-id`

   访问 `WhateverGreen` 官方文档可以查到，不过 `OpenCore` 的文档也是不错的选择。

   |来源|链接|
   |:-|:-|
   |`WhateverGreen`|https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.cn.md|
   |`OpenCore`|https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/intel-gpu.html#native-intel-igpus<br>https://dortania.github.io/GPU-Buyers-Guide/legacy-gpus/legacy-intel.html#sandy-bridge-i3-5-7-2xxx|

   这里要注意的是，在 `WhateverGreen` 文档中“建议”那一节要仔细看看。

1. 确定机型

   这里要感谢黑果小兵的分享
   
   https://blog.daliansky.net/Intel-core-display-platformID-finishing.html

## Nvidia

不论“免驱”还是“需要驱动”，都需要 `Lilu` 和 `WhateverGreen`。“需要驱动”指的是需要安装 nvidia 的 webdriver。

1. 确定显卡可以驱动

   查表

   OpenCore 文档
   - https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/nvidia-gpu.html
   - https://dortania.github.io/GPU-Buyers-Guide/legacy-gpus/legacy-nvidia.html

   小兵
   - https://blog.daliansky.net/Mojave-Hardware-Support-List.html

   可以查到以下内容
   - 是否“免驱”
   - 支持的操作系统版本

## AMD

AMD 的显卡只有“免驱”和“无解” 2 中情况。当然仍旧需要 `Lilu` 和 `WhateverGreen`。

1. 确定显卡可以驱动

   查表

   OpenCore 文档
   - https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/amd-gpu.html
   - https://dortania.github.io/GPU-Buyers-Guide/legacy-gpus/legacy-amd.html

   小兵
   - https://blog.daliansky.net/Mojave-Hardware-Support-List.html

   可以查到以下内容
   - 是否可以驱动
   - 支持的操作系统版本

## `config.plist` 文件编写

我们来看看 intel 核显在 `config.plist` 中的配置。虽然 OC 和 Clover 的 `config.plist` 文件结构是不同的，但是“键（key）”和“键值（key value）”是一样的。

1. 键

   阅读 `WhateverGreen` 文档中“使用 WEG 自定义 FB 和 端口 补丁”小节

   https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.cn.md

1. 键值

   这里会遇到 2 个问题
   1. 如果直接用“记事本”之类的文档编辑器打开 `config.plist` 文件，会发现“键值”是看不懂的，因为它经过了 `Base64` 编码，所有不是给人看的。

      解决方法：使用专用的编辑器，例如：`ProperTree`
   
   1. 键值的书写规范

      键值的书写是有要求的，我们前面查到的值，在编辑器中书写时要反过来写，而且是 2 位的。

      例如：那个所谓的万能 id，`0x12345678`。首先，前面的 `0x` 是 16 位前缀，不用管它。接下来 2 位 2 位的翻转，结果就是 `78563412`。

      示例：是/否
      - 我们以 `framebuffer-patch-enable` 示例，该键是“启用语义补丁的总开关”。如果开启，那么值就是 1（0x00000001），转换后键值为 `01000000`。

      示例：显存
      - 我们以 `framebuffer-unifiedmem` 为例，设置显存为 2048MB（2GB）。用计算器算下 `2048M=2*1024*1024*1024=2147483648`，转 16 进制为 `0x80000000`，转换后键值为 `00000080`。