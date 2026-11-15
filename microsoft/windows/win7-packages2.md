# Windows 7 补丁

- 最小化补丁集合
- 重要的补丁
- IE11 及相关补丁
- .NET Framework 3.5.1 相关补丁

## Windows 7 x64 最小化补丁集合

|KB|分类|描述|最后更新|
|:--|:--|:--|--:|
|KB3020369|SSU|KB3125574 的专用前置 SSU|2015.05.12|
|KB4490628|服务堆栈更新|服务堆栈更新（SSU）|2019.03.12|
|KB4474419|安全|SHA-2 代码签名支持|2019.09.10|
|KB3125574|更新|面向 Win7 SP1 的“便捷汇总”，包含了 SP1 发布后到 2016 年 4 月所有非安全更新|2016.05.17|
|KB3140245|更新|TLS 1.2 功能|2016.06.14|
|KB3172605|更新|后续 TLS 协议的可靠性修复补丁|2016.09.13|
|KB4534310|安全|Windows 7 官方免费通道的最后一个月度安全质量汇总，2020 年 1 月|2020.01.14|


```
----2900986 ActiveX Killbits 的累积安全更新，属于微软安全公告 MS13-090，专门针对 Windows 7 上的 Internet Explorer。
----3185319 for IE11

4041083 2017-09 .NET 3.5.1 - 4.7 安全和质量汇总
4049016 2017-11
4535102 2020-01 .NET 3.5.1 - 4.8 安全和质量汇总该更新后续已被 2020 年 5 月的 KB4556399 取代。

----2912390
----3035126
2631813 被取代
----3156016
```

```
开始
--------------------------------------------------------------------
976902
2534111
---------------------------------------------------------------------
3020369----KB5017397
3125574
3140245
3172605
4474419
4490628
4534310
--------------------------------------------------------------------
2667402----
2698365----
2706045----IE9 及以上不适用
2862330----
2912390
2984972----
3004375----3031432
3031432----（显示为）3004375
3035126
3046269----
3059317----
3110329
3150220----4534310
3155178----
3156016----
3159398----
3161949----
---------------------------------------------------------------------
????

????
-----------------------------------------------------------------------
？----2533552（）
4019990
4532945
------------------------------------------------------------------------
2900986
------------------------------------------------------------------------
IE11
------------------------------------------------------------------------
2670838
2729094
2834140
？----4040980（被 KB4532945 替代）
？----4524752（支持终止提醒）
-------------------------------------------------------------------------
2685811 内核模式驱动程序框架（KMDF）1.11 版更新
2685813 内核模式驱动程序框架（KMDF）1.11 版更新
-------------------------------------------------------------------------
2894844
3185319
2912390
3035126
3110329
--------------------------------------------------------------------------



----------------------------------------------------------------------------
结束


```

## 重要的补丁

|KB|分类|描述|最后更新|
|:--|:--|:--|--:|
|KB3004375|安全|主要功能是增强命令行审核（Command Line Auditing）|2015.02.10|
|KB3031432|安全|修复 Windows 进程创建时权限提升漏洞（CVE-2015-0062）|2015.05.14|
|KB2698365|安全|属于安全公告 MS12-045，用于修复 Microsoft 数据访问组件（MDAC）中一个可能允许远程代码执行的安全漏洞。|2014.09.02|
|KB2984972|安全|为本地安全机构（LSA）提供额外保护，并为凭据安全支持提供程序（CredSSP）及远程桌面连接引入“受限管理模式”，旨在防范凭据窃取 。|2014.10.14|
|KB3155178|安全|修复 Windows Journal 中的一个远程代码执行漏洞（CVE-2016-0182）。|2016.05.10|
|KB2667402|安全|修复了 RDP 中的两个漏洞。|2014.09.02|
|KB2706045|安全|修复 JScript 与 VBScript 脚本引擎远程代码执行漏洞的安全更新。|2014.09.02|
|KB2862330|安全|修复 USB 驱动漏洞|2014.01.14|
|KB3046269|安全|修复任务计划程序权限提升漏洞|2015.04.14|
|KB3059317|安全|修复 Microsoft 通用控件漏洞|2015.06.09|
|KB3156016|安全|修复 Microsoft 图形组件漏洞|2016.05.10|
|KB3159398|安全|修复组策略权限提升漏洞|2016.06.14|
|KB3161949|安全|修复 WPAD（Web 代理自动发现协议）权限提升漏洞|2016.06.14|
|KB2533552|更新|KB976932 中|2011.05.31|

|KB2894844|安全|.NET Framework 3.5.1 的安全更新|2014.09.09|
|KB4019990|更新|更新 d3dcompiler_47.dll 组件。.NET 4.7）的安装前提条件。|2017.05.30|
|KB4040980|安全|KB4049016 中，||
|KB4532945|安全|.NET Framework 3.5.1 的安全与质量汇总更新|2020.01.14|

|KB2900986|安全|ActiveX Killbits 的累积安全更新|2013.11.12|

|KB2670838|Feature Pack|平台更新，安装 Internet Explorer 10/11 的一项前提条件|2013.03.12|
|KB2729094|更新|字体更新，升级到 Internet Explorer 11 的一项前提条件|2014.09.02|
|KB2834140|更新|解决安装 KB2670838 后蓝屏，为安装 Internet Explorer 11 的一项前置必备更新|2013.10.08|
|IE11|||2014.04.22|
|IE11 zh-CN 语言包||||
|||Microsoft Windows English Spelling Package||
|||Microsoft Windows English Hyphenation Package||
|KB3185319|安全|Internet Explorer 11 的累积安全更新|2016.09.13|
|KB2912390|安全|Direct2D 组件的严重级别安全更新，需要先安装 KB2670838|2014.02.11|
|KB3035126|安全|修复 Windows 照片解码器组件中的信息泄露漏洞|2015.03.10|
|KB3110329|安全|解决 Windows 内核模式驱动中的多枚高危漏洞|2016.01.12|

```
--------------------------------------------------------------------
4503548 Microsoft .NET Framework 4.8 的安装程序/功能包


3138612 更新 Windows Update 客户端（Windows Update Client）


---------------------------------------------------------------------
----4524752 Win7终止支持提醒补丁

----2894844

---------------------------------------------------------------------
21 个“更新程序”
```



```text
D:\mkos\packages\windows-7-sp1-x64-packages\0.SSU\windows6.1-kb4490628-x64_d3de52d6987f7c8bdc2c015dca69eac96047c76e.msu
D:\mkos\packages\windows-7-sp1-x64-packages\1.KB3125574\windows6.1-kb3125574-v4-x64_2dafb1d203c8964239af3048b5dd4b1264cd93b9.msu
D:\mkos\packages\windows-7-sp1-x64-packages\2.KB4474419\windows6.1-kb4474419-v3-x64_b5614c6cea5cb4e198717789633dca16308ef79c.msu
D:\mkos\packages\windows-7-sp1-x64-packages\3.0.IE11-Pre\windows6.1-kb2670838-x64_9f667ff60e80b64cbed2774681302baeaf0fc6a6.msu
D:\mkos\packages\windows-7-sp1-x64-packages\3.0.IE11-Pre\windows6.1-kb2729094-v2-x64_e1a3ecc5030a51711f558f90dd1db52e24ce074b.msu
D:\mkos\packages\windows-7-sp1-x64-packages\3.0.IE11-Pre\windows6.1-kb2834140-v2-x64_3db9d9b3dc20515bf4b164821b721402e34ad9d6.msu
D:\mkos\packages\windows-7-sp1-x64-packages\3.1.IE11\IE-Win7.CAB
D:\mkos\packages\windows-7-sp1-x64-packages\3.1.IE11\ielangpack-zh-CN.CAB
D:\mkos\packages\windows-7-sp1-x64-packages\3.1.IE11\IE-Spelling-en.MSU
D:\mkos\packages\windows-7-sp1-x64-packages\3.1.IE11\IE-Hyphenation-en.MSU
D:\mkos\packages\windows-7-sp1-x64-packages\4.Monthly-Rollup-2020.01\windows6.1-kb4534310-x64_4dc78a6eeb14e2eac1ede7381f4a93658c8e2cdc.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\ie11-windows6.1-kb3185319-x64_fc0fd52e6ce28c212c2ce5b3dd13cf5fbcb95ca5.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb2533552-x64_0ba5ac38d4e1c9588a1e53ad390d23c1e4ecd04d.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb2667402-v2-x64_15c04bd5944cd9b34a294a25b96911057593c465.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb2698365-x64_f3ad859582ad240c95b9ed867bc9b99e39d15ba9.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb2862330-v2-x64_c1a8b768d8c22640d0a80966d124f441eb625934.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb2900986-x64_a56afda70b8208665280cb79d0a6704bb7dcc3bb.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb2912390-x64_413ad3ebc0199bd6d0ec00aaa0a17c73a00b8c30.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb2984972-x64_2545620eadc06a0a3fd426b5853b2e0b48187599.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3004375-v3-x64_c4f55f4d06ce51e923bd0e269af11126c5e7196a.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3031432-x64_e648abe279c8b0095a57271ffbab5d5d376da558.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3035126-x64_ba6bf5118bc60be7f824c4dba9131185e4755646.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3046269-x64_9cdabeb9c2a859414c27c4f981d6b1334aee0ad5.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3059317-x64_b68db33239bddcb59e881252cfc7b79d58a2f26b.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3110329-x64_4ed9eebee2938cf8c55550e2a7f196a409e80b76.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3155178-x64_5db0e41e4bb12253f5c9f9bc5c1431b1b6073bf8.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3156016-x64_97fa9ecb5f3a03a0739c6baeea3d9371c1474a6a.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3159398-x64_dc2b2c11af4b38b0b632bd7f6d683d57a93b711c.msu
D:\mkos\packages\windows-7-sp1-x64-packages\5.Security-Update\windows6.1-kb3161949-x64_e2372fb5746e9474cec6ef1710f8d58ec5c6c000.msu
D:\mkos\packages\windows-7-sp1-x64-packages\6.NET-Framework\windows6.1-kb2894844-x64_71b051d4b2eae12423868e28b0e5b04a9e10c048.msu
D:\mkos\packages\windows-7-sp1-x64-packages\6.NET-Framework\windows6.1-kb4019990-x64_35cc310e81ef23439ba0ec1f11d7b71dd34adfe5.msu
D:\mkos\packages\windows-7-sp1-x64-packages\6.NET-Framework\windows6.1-kb4040980-x64_83282fb5210091802984ead0d4175879056d602c.msu
D:\mkos\packages\windows-7-sp1-x64-packages\6.NET-Framework\windows6.1-kb4532945-x64_d070fb06c4c56f70e4d2e891181028fa7c35694d.msu
D:\mkos\packages\windows-7-sp1-x64-packages\7.Update\windows6.1-kb3172605-x64_2bb9bc55f347eee34b1454b50c436eb6fd9301fc.msu
```