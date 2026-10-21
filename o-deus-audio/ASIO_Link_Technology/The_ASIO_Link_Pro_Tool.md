# The ASIO Link Pro Tool

这既是一个配置工具，也是一个简单的 ASIO 主机应用程序，用于对 ASIO Link Pro 进行配置和测试。由于您可以完全掌控所有 ASIO 设置，因此在排查和诊断问题时会非常有用。

此外，它还可以清除主机应用程序的所有默认设置。如果您希望重新开始，这相当于进行一次全新安装。

## Using the ASIO Link Pro Tool

![](../_media/23-1.jpg)  
_ASIO Link Pro Tool UI_

## ASIO Link Pro Tool Functions

### ASIO Settings

|||
|:--|:--|
|**Sample rate** |要设置的 ASIO 采样率。“ASIO preferred（ASIO 首选）”为默认值，将使用 ASIO 驱动程序的默认采样率。|
|**Buffer size** |尝试在驱动程序中设置的 ASIO 缓冲区大小。<br>如果需要低延迟（较小的缓冲区大小意味着更低的延迟），请尽量将其设得尽可能小；但若设置过小，音频可能会失真。<br>“ASIO preferred（ASIO 首选）”为默认值，将使用 ASIO 驱动程序的首选缓冲区大小。|
|**Channels IN/OUT** |选择输入和输出通道的数量。|
|**Init ASIO<br>** |初始化 ASIO Link Pro 驱动程序，但不会启动它。|
|**START ASIO<br>** |启动 ASIO Link Pro 驱动程序的音频处理，您还可以使用测试音来测试您的 ASIO 驱动程序。|
|**Stop ASIO<br>** |停止 ASIO Link Pro 驱动程序。|
|**ASIO CPanel** |打开 ASIO 驱动程序的控制面板。|
|**Test tone** |向所有已启用的 ASIO 输出通道播放 440Hz 的测试音。|
|**Send IN to OUT** |ASIO Link Pro 工具会将音频从 ASIO 输入路由至 ASIO 输出。<br>此选项仍保留在内，但您可以在 ASIO Link Pro 驱动程序中以任意方式对音频进行路由。|

### Tool Settings

|||
|:--|:--|
|**Start minimised and START ASIO** |启用后，ASIO Link Pro 工具将以最小化状态驻留在系统托盘，并自动启动 ASIO Link Pro。如果您希望随 Windows 启动 ASIO Link Pro，此选项将非常有用。|
|**Start with windows** |启用后，ASIO Link Pro 工具将随 Windows 自动启动。通常，您还应同时启用“Start minimised and START ASIO（最小化启动并启动 ASIO）”选项，以便实现 ASIO Link Pro 的自动启动。|

### ASIO Link Settings

|||
|:--|:--|
|**Start ASIO Link Pro minimised** |以最小化形式在系统托盘中启动 ASIO Link Pro 驱动程序，直到单击托盘图标时才会弹出用户界面。|
|**Do not check for updates** |ASIO Link Pro 将不再提示您是否有可用的更新。|
|**Allow ASIO Link Pro to get focus** |允许 ASIO Link Pro 成为激活或获得焦点的窗口。默认情况下未启用此选项，是因为 ASIO Link Pro 可能会抢占主机应用程序或 DAW 的焦点，从而导致这些程序自动关闭 ASIO 驱动程序！一旦发生这种情况，ASIO Link Pro 就会被主机“关闭”。启用此选项时请务必谨慎，并参阅[常见问题](FAQ.md)解答。|
|**Enable LOOPER loopback racks** |ASIO Link Pro 将显示两个额外的机架，分别命名为 LOOPER IN 和 LOOPER OUT，用于将音频回送以作为输入使用。|
|**Enable second NETWORK IN/OUT** |ASIO Link Pro 现在将显示两个额外的网络机架，分别命名为 NETWORK IN 2 和 NETWORK OUT 2，用于实现与另一台设备之间的音频收发。|

### ASIOVADPRO (WDM) settings

|||
|:--|:--|
|**WDM test tone** |向首个ASIOVADPRO speakers 播放立体声 880Hz 测试音调。|
|**WinMM CPanel** |启动 Windows 多媒体控制面板。|
|**Use strict ASIO clock** |ASIOVADPRO WDM 驱动程序通常会采用平滑处理，以平均 ASIO 时钟与自身 DPC 时钟的时间。启用“Use strict ASIO clock（严格ASIO时钟）”后，ASIOVADPRO 将仅使用 ASIO 时钟。|
|**Auto-set audio wave format** |当使用 ASIO Link Pro 时，ASIOVADPRO 的采样率（sample rate）和位深度（bit format）将自动设定（Windows XP系统下不可用）。|
|**Auto-set as default audio device** |在使用 ASIO Link Pro 时，ASIOVADPRO 将被自动设为默认的音频播放和录音设备（Windows XP系统下不可用）。|
|**Allow 32 bit PCM format** |如果 ASIO 驱动程序使用 32 位波形格式，ASIOVADPRO 也将采用 32 位波形格式。此设置要求同时启用“Auto-set audio wave format（自动设置 ASIOVADPRO 波形格式）”选项（Windows XP系统下不可用）。|

### Miscellaneous

|||
|:--|:--|
|**About** |显示“关于”对话框。|
|**Reset settings** |清除 ASIO Link Pro 和 ASIO Link Pro 工具的所有已保存设置。|
|**Exit** |退出 ASIO Link Pro 工具。|