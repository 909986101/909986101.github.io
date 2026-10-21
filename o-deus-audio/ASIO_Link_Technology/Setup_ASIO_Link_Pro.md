# Setup ASIO Link Pro

## Run ASIO Link Pro Tool

安装完成后，安装程序通常会自动启动 [ASIO Link Pro Tool](The_ASIO_Link_Pro_Tool.md)。建议点击“START ASIO”按钮，进行一次简单测试，以确认 ASIO Link Pro 已正确安装。此后，您即可在常用的宿主软件中运行 ASIO Link Pro。 

## Choose ASIO Link Pro in Host ASIO Settings

**在主机的 ASIO 设置中选择“ASIO Link Pro”**

安装完成后，您可以启动您的 DAW 或 ASIO 主机应用程序。本演示以 Ableton Live 8 为例，但各 DAW 在 ASIO 配置方面大同小异。

首先，在音频偏好设置中将驱动程序类型选为 ASIO，并将音频驱动设备选为“ASIO Link Pro”。

当该主机程序首次运行 Link 时：

|ASIO driver 数量|ASIO Link Pro 动作|
|:--|:--|
|1 |自动将其选为默认驱动 |
|多个 |将会弹出一个小型下拉列表（见下图），供您选择所需的驱动程序 |
|无 |将使用“ASIO Link Pro Null Driver”，这是一款仅用于网络通信的静默驱动。<br>如果您看到此提示，我们建议您改用 _ASIO4ALL_。

> 提示：您随时可以通过 ASIO Link Pro 界面中的“选择驱动”按钮更换新的驱动程序。

![](../_media/7-1.jpg)  
_Select ASIO Link Pro in your host app and select the ASIO driver_

接下来，如果图形界面未自动弹出，请单击系统托盘中的新绿色（或紫色）图标。

![](../_media/7-2.jpg)  
_Tray Icon_

现在，在 ASIO Link Pro 的图形用户界面中，请查看采样率（sample rate），因为在下一步中您需要这一信息。

_最好以尽可能低的 ASIO 延迟运行，10 毫秒或更短为佳！_

## Setup the ASIOVADPRO Devices

_除非您使用的是 Windows XP，否则在 Windows Vista 及更高版本的操作系统中，除设置扬声器配置外，其他操作均可自动完成。_

### Windows Multimedia Control Panel

要访问此面板，请右键单击 Windows 任务栏中的扬声器图标，然后选择“播放设备”或“录音设备”。

![](../_media/8-1.jpg)  
Windows speaker tray icon

“播放”选项卡包含 ASIOVADPRO Speakers 01-04，“录制”选项卡则包含 ASIOVADPRO Mix 01-04。

_You can also access this control panel with the ![](../_media/8-2.jpg)  button in ASIO Link Pro_

#### Default Device

要使 Windows 通过 ASIO Link Pro 输出并接收所有音频，您需要将 ASIOVADPRO Speakers 01 和 ASIOVADPRO Mix 01 设置为 Windows 的默认设备 _**（在 Vista、7、8 和 10 中为自动设置）。**_

![](../_media/8-3.jpg)  
_ASIOVADPRO Speakers and Mix audio devices_

#### Default Format

下一步是右键单击每个设备，进入其属性设置，并确保采样率与您所使用的 ASIO 采样率一致 _**（在 Vista、7、8 和 10 系统中为自动设置）。**_

要确认 ASIO 采样率，请查看 ASIO Link Pro 的界面状态栏（help bar）以获取当前的采样率。

![](../_media/8-4.jpg)  
_ASIO Link Pro UI Settings and Help bar sections_

![](../_media/9-1.jpg)  
_ASIOVADPRO Default Format properties_

您只需确认默认格式与 ASIO Link Pro 所使用的格式一致即可。位深（bits）可设为任意值，但通常 24 bit（位）已完全足够。

#### Speaker Configuration

重要的是，您需要告知 Windows 使用正确的扬声器配置。请右键单击 ASIOVADPRO Speakers（扬声器播放设备），然后选择“配置扬声器（Configure Speakers）”，您将看到如下界面，在这里可以根据您的需求选择合适的配置。

默认情况下，已选择 7.1 声道配置。

![](../_media/10-1.jpg)  
_Configure ASIOVADPRO Speakers Setup_
