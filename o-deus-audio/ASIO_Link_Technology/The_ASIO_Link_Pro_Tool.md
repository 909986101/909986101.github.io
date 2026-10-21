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
|**Sample rate<br>（采样率）** |要设置的 ASIO 采样率。“ASIO preferred（ASIO 首选）”为默认值，将使用 ASIO 驱动程序的默认采样率。|
|**Buffer size<br>（缓冲区大小）** |尝试在驱动程序中设置的 ASIO 缓冲区大小。<br>如果需要低延迟（较小的缓冲区大小意味着更低的延迟），请尽量将其设得尽可能小；但若设置过小，音频可能会失真。<br>“ASIO preferred（ASIO 首选）”为默认值，将使用 ASIO 驱动程序的首选缓冲区大小。|
|**Channels IN/OUT<br>（输入/输出通道数）** |选择输入和输出通道的数量。|
|**Init ASIO<br>（初始化 ASIO）** |初始化 ASIO Link Pro 驱动程序，但不会启动它。|
|**START ASIO<br>（启动 ASIO）** |启动 ASIO Link Pro 驱动程序的音频处理，您还可以使用测试音来测试您的 ASIO 驱动程序。|
|**Stop ASIO<br>（停止 ASIO）** |停止 ASIO Link Pro 驱动程序。|
|**ASIO CPanel<br>（ASIO 控制面板）** |打开 ASIO 驱动程序的控制面板。|
|**Test tone<br>（测试音）** |向所有已启用的 ASIO 输出通道播放 440Hz 的测试音。|
|**Send IN to OUT<br>（发送 IN 至 OUT）** |ASIO Link Pro 工具会将音频从 ASIO 输入路由至 ASIO 输出。<br>此选项仍保留在内，但您可以在 ASIO Link Pro 驱动程序中以任意方式对音频进行路由。|

### Tool Settings

**Start minimised and START ASIO（最小化启动并启动 ASIO）**——启用后，ASIO Link Pro 工具将以最小化状态驻留在系统托盘，并自动启动 ASIO Link Pro。如果您希望随 Windows 启动 ASIO Link Pro，此选项将非常有用。

**Start with windows（随 Windows 启动）**——启用后，ASIO Link Pro 工具将随 Windows 自动启动。通常，您还应同时启用“Start minimised and START ASIO（最小化启动并启动 ASIO）”选项，以便实现 ASIO Link Pro 的自动启动。

### ASIO Link Settings

**Start ASIO Link Pro minimised** – Start the ASIO Link Pro driver minimised to the system tray so the UI does not pop up till the tray icon is clicked.

**Do not check for updates** – ASIO Link Pro will no longer prompt you if you an update is available

**Allow ASIO Link Pro to get focus** – Allows the ASIO Link Pro to become the activated/focused window. The reason this is not enabled by default is that the ASIO Link Pro can take focus away from host applications or DAWs that auto- close the ASIO driver! When this happens, ASIO Link Pro gets "closed" by the host. Be careful if you enable this and read the FAQ below.

**Enable LOOPER loopback racks** – ASIO Link Pro will show two additional racks named LOOPER IN and LOOPER OUT to allow sending audio back to for use as an input.

**Enable second NETWORK IN/OUT** – ASIO Link Pro will now show two additional networking racks named NETWORK IN 2 and NETWORK OUT 2 to allow sending/receiving audio from another machine.

### ASIOVADPRO (WDM) settings

**WDM test tone** – Plays a stereo 880Hz test tone to the first ASIOVADPRO speakers.

**WinMM CPanel** – Launches the windows multimedia control panel.

**Use strict ASIO clock** – The ASIOVADPRO WDM driver normally uses smoothing to average out the ASIO clock time and its own DPC clock time. When strict ASIO clock is enabled ASIOVADPRO uses only the ASIO clock.

**Auto-set audio wave format** – The ASIOVADPRO sample rate and bit format will be automatically set when ASIO Link Pro is in use (not available in Windows XP).

**Auto-set as default audio device** – ASIOVADPRO will be automatically set as the default audio playback and recording devices when in ASIO Link Pro is in use (not available in Windows XP).

**Allow 32 bit PCM format** – ASIOVADPRO will use 32 bit wave format if the ASIO driver is using 32bit wave format. This setting requires Auto-set ASIOVADPRO wave format to be enabled (not available in Windows XP).

### Miscellaneous

**About** – Shows an "About" dialog box.

**Reset settings** – Clears all saved settings for ASIO Link Pro and ASIO Link Pro Tool.

**Exit** – Exits the ASIO Link Pro Tool.
