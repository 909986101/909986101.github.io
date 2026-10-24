# VB-Audio Matrix & Coconut 用户手册

<div style="width: 50%; margin: 0 auto; text-align: center;">

<p><strong>Windows 通用音频路由器</strong></p>

![](VBMatrix_UserManual/matrix-1-1.jpg)

</div>

> 官方网站 [www.vbaudiomatrix.com](https://www.vbaudiomatrix.com)

本文档介绍了 VB-Audio Matrix（VBMatrix）及其增强版本（Coconut）中的所有功能。

# 安装

- 运行安装程序并按照提示操作。

- 安装或卸载完成后，请重新启动系统。

## 首次安装

> 作为先决条件，您可能需要具备管理员权限；否则，请以管理员模式运行安装程序。

1. 运行安装程序，然后单击“安装（INSTALL）”按钮。

2. 如果已安装，请单击“卸载（REMOVE）”按钮。

3. 每次操作后请**重启计算机（非常重要）**。  
**（虚拟音频设备驱动程序需要此重启才能完成卸载或安装）**

## 更新

更新前请先卸载 VBMatrix。您可以在更新前将当前设置保存到文件中，但通常情况下无需修改（安装程序不会删除现有设置）：

作为前提条件，您可能需要具备管理员权限；否则，请以管理员身份运行安装程序。请关闭所有可能使用 VBMatrix 的应用程序。

1. 运行安装程序，然后点击“卸载”按钮。

2. 重启计算机（重要）

### 重新安装之前，您可以检查以下几点

- 在 Windows 设备管理器中，确保所有 VBMatrix VAIO 虚拟音频驱动程序均已卸载（分别在“游戏控制器”和“音频输入/输出”部分查看）。如果仍有残留，您需要从相应位置手动卸载（右键单击以调出菜单选项）。

### 重新安装

3. 运行安装程序，点击“安装（INSTALL）”按钮。

4. 之后请重启（重要）

### 然后您可能

5. 检查 Windows 的音频设置（默认播放设备、默认录音设备等）

6. 检查软电话（soft phone）的设置（例如 Skype、Zoom 或 Discord 的音频设备选择）。

7. 运行所需的 VBMartrix 版本，并在防火墙提示时进行授权（如果 VBAN 服务正在运行）。

8. 也可能需要再次检查菜单中的某些选项（系统托盘、开机自启、启动时显示应用等）。

# 在线支持（ONLINE SUPPORT ）

[https://vb-audio.com/Services/support.htm](https://vb-audio.com/Services/support.htm)

# Fair Trade, Affordable For Everyone

VB-Audio Matrix 以捐赠软件（Donationware）的形式发布，并附带激活码！30天试用期结束后，软件将定期提示您激活许可证。

如用于专业用途，您可在我们的网上商店按建议的许可价格购买；如需批量授权或商业发行，请联系我们获取报价或签订协议。

更多许可信息: [https://vb-audio.com/Services/licensing.htm](https://vb-audio.com/Services/licensing.htm)

软件商店：  
[https://shop.vb-audio.com](https://shop.vb-audio.com)

Windows XP (SP2), VISTA, WIN7, WIN8, WIN8.1, WIN10/11 32/64 bits ARM64 compatible (MME, DX, WDM/WASAPI, KS, ASIO).

# 引言

VB-Audio Matrix 是一款适用于 Windows 的通用音频路由器，能够通过不同的音频接口同时管理多个 ASIO 设备、多个 Windows 音频设备、多个音频应用程序、多个 ASIO 应用程序或 VBAN 流，并具备将任意输入路由至任意输出（即任意源到任意目标）的能力，且可按通道进行配置。

![](VBMatrix_UserManual/matrix-6-1.jpg)

VB-Audio Matrix 最多可管理 128 个 ASIO 设备通道和 64 个 VBAN 流通道，并提供完整的路由网格视图、预设管理、MIDI 功能以及 VBAN-TEXT 请求功能。

VB-Audio Matrix Coconut 则提供更多插槽，最多可管理 512 个 ASIO 设备通道、128 个 VBAN 流通道以及 64 个 Windows 设备通道。

主采样率（main sample rate）与缓冲（buffering）设置显示在 VDSP/CPU 负载指示条下方。

![](VBMatrix_UserManual/matrix-6-2.jpg)

# Matrix 插槽（Slots）

VB-Audio Matrix 提供了 5 种类型的插槽（slots）：

**ASIO Devices（ASIO 设备）：** 用于选择 ASIO 驱动程序（每个插槽最多支持128个通道，具体数量受限于插槽规格）。

**Windows Devices（Windows 设备）：** 用于选择 Windows 设备（最多支持8个通道）。

**VAIO：** 用于使用随 Matrix 安装的虚拟音频输入/输出功能（适用于 Windows 10/11 64位或 ARM64 系统）。

**VBAN Streams（VBAN 流）：** 用于通过 VBAN 协议与其他计算机之间发送或接收音频流。

**Virtual ASIO（虚拟 ASIO）：** 用于使用随 VB-Audio Matrix 安装的虚拟 ASIO 驱动程序。

![](VBMatrix_UserManual/matrix-7-1.jpg)

按住 Ctrl 键并单击，可在插槽中选择设备或启用该插槽。

**一旦启用某个插槽（Slot），它就会显示在路由网格（Routing Grid）中。**

# 路由网格（Routing Grid）

点击 MATRIX 标志或使用菜单中的“Routing Grid（路由网格）”选项，即可进入 Matrix 路由网格（Routing Grid）：

![](VBMatrix_UserManual/matrix-8-1.jpg)

这使得能够将任意输入路由至任意输出，且可设置增益。换言之，它允许将任意信号源发送至任意目标。

一个区域（Zone）可以被定义为执行不同的操作（例如重置各点或将其存储到所选预设中），也可以同时作用于该区域内的所有点（例如将增益设置为 0dB）。

一个预设由最多64个区域中的任意数量的点组成。预设一经定义，即提供一个滑动增益调节器 / Slider Gain（用于设定所有点的最大电平）、一个应用（Apply）按钮（当预设完全生效时显示绿色）、一个静音（Mute）按钮以及一个相位（Phase）按钮（用于反转相位）。

选项（Options）菜单提供了多种显示模式：三种不同的视图和轴向选项，可根据需要选择垂直或水平方向的输入/输出显示。

鼠标滚轮可用于在网格中上下移动（按住Shift键则可水平移动）。  
方向键也可用于浏览网格：
- Ctrl + 方向键可按页移动；  
- Ctrl + 方向键可在各点之间移动；
- Shift + 方向键可在不同槽位之间切换。

## 预设音色（Preset Patch）

Matrix 提供了一组 64 个永久预设，这些预设会自动存储在磁盘上（位于“我的文档\\VBAudioMatrix\\PresetPatch”目录下）。

要修改某个预设，首先需选中该预设，然后在矩阵上定义一个区域（或选定一个点），再右键单击，即可在上下文菜单中选择“存储或添加当前点/区域到所选预设”（一个预设最多可包含 64 个区域）。所选预设中的各点将以浅蓝色显示。

![](VBMatrix_UserManual/matrix-9-1.jpg)

<div style="display: grid; grid-template-columns: 4.5fr 0.5fr 5fr;">
  <div>
  
  ![](VBMatrix_UserManual/matrix-9-2.jpg)
  
  </div>
  <div></div>
  <div>
    <p>右键单击预设（Preset）即可调出功能列表。 </P>
    <p>Recall preset（调用预设）：将预设应用于指定区域（该操作会移除区域内所有不属于该预设的点）。其他功能，如应用、增益、静音、相位（Apply, Gain Mute, Phase）等，仅作用于预设中的点；若某点不在预设范围内，则不会对其产生影响。</P>
    <p>每个预设均可设置名称（Name）和备注（Comment）。</P>
    <p>Update Preset（更新预设）：以当前点的数值与状态恢复预设，并自动将其置为已应用状态。“A”按钮在预设中所有点均按预设定义设置完毕时呈全绿色。</P>
  </div>
</div>

# 系统设置（System settings）

通过菜单（或按 Ctrl + ,）即可打开系统设置（system settings）对话框，以查看各项选项：

![](VBMatrix_UserManual/matrix-10-1.jpg)

缓冲区（Buffering）可针对不同的音频接口进行设置：MME、WDM（WASAPI）、KS、ASIO，以及内部时钟。

首选的主设备采样率（Preferred mains sample rate）和缓冲区大小会与每个设备协商确定。但最终，设备仍可能提出其他格式或缓冲区大小。

虚拟 ASIO 驱动程序严格（strictly）同步于主设备，因此会自动采用主设备的采样率和缓冲区大小。VAIOs 会自动将主设备的采样率作为内部采样率，而 VAIO 的缓冲区大小则可通过主界面进行设置。

VAIOs 同步模式（VAIOs Synchronization）可强制 VAIO Windows 驱动程序严格同（strictly）步于主时钟（从而有望提升 VAIO 流的稳定性并使其与主设备保持同步）。

## 对讲设备插槽（TALKBACK Device Slot）

显示用于在特定 I/O（录音设备）及该设备的通道上进行对讲的设备。默认情况下，对讲可通过连接在 WIN1.IN 插槽中的录音设备实现。

## 监听设备插槽（MONITOR Device Slot）

显示用于监听特定输入/输出（播放设备）以及该设备声道的设备。默认情况下，监听可通过连接在 WIN1.OUT 插槽中的播放设备实现。

# 日志/命令行（LOG / CLI）

VB-Audio Matrix 还提供了一个日志/CLI 窗口，便于您查看系统运行情况以及所使用的事件或命令。您可以在底部的编辑框中输入 CLI（命令行指令），并通过“send（发送）”按钮将其发出：

![](VBMatrix_UserManual/matrix-11-1.jpg)

这也是获取请求语法的实用方法。大多数指令也可以用作 VBAN-TEXT 请求。

## 命令行指令集（Command Line Instruction Set）

SUID = Slot unique identifier (e.g. ASIO128, VBAN1 etc…).

```
Point(SUID.IN[i], SUID.OUT[j]).dBGain = -6.0; 
Point(SUID.IN[i1..i2], SUID.OUT[j1..j2]).dBGain = -6.0;

Point(SUID.IN[i], SUID.OUT[j]).Remove;  //Remove point 
Point(SUID.IN[i1..i2], SUID.OUT[j1..j2]).Remove;

Point(SUID.IN[i], SUID.OUT[j]).Mute = 1; 
Point(SUID.IN[i1..i2], SUID.OUT[j1..j2]).Mute =1;

Point(SUID.IN[i], SUID.OUT[j]).Phase = 1; 
Point(SUID.IN[i1..i2], SUID.OUT[j1..j2]).Phase =1;

Point(SUID.IN[i], SUID.OUT[j]).Paste;   //see Zone().Copy

Undo; 
Redo;

Output(SUID.OUT[j]).Name = "MyName";    //set label 
Output(SUID.OUT[j1..j2]).Name = "";     //to remove label

Output(SUID.OUT[j]).Reset;              //Remove all points 
Output(SUID.OUT[j1..j2]).Reset;

Input(SUID.IN[i]).Name = "MyName";      //set label 
Input(SUID.IN[i1..i2]).Name = "";       //to remove label

Input(SUID.IN[i]).Reset;                //Remove all points 
Input(SUID.IN[i1..i2]).Reset;

Zone(SUID.IN[i], SUID.OUT[j\]: SUID.IN[k], SUID.OUT[l]).Reset; 
Zone(SUID.IN[i], SUID.OUT[j\]: SUID.IN[k], SUID.OUT[l]).Copy; 
Zone(SUID.IN[i], SUID.OUT[j\]: SUID.IN[k], SUID.OUT[l]).Store = nuPreset; 
Zone(SUID.IN[i], SUID.OUT[j\]: SUID.IN[k], SUID.OUT[l]).Add = nuPreset;

Zone(SUID.IN[i], SUID.OUT[j\]: SUID.IN[k], SUID.OUT[l]).dBGain = -6.0; 
Zone(SUID.IN[i], SUID.OUT[j\]: SUID.IN[k], SUID.OUT[l]).Mute = 1; 
Zone(SUID.IN[i], SUID.OUT[j\]: SUID.IN[k], SUID.OUT[l]).Phase = 1;

Slot(SUID.IN).Reset = 1; 
Slot(SUID.OUT).Reset = 1; 
Slot(SUID).Reset = 1; 
Slot(SUID).Online = 1; 
Slot(SUID).Master = 1;

Slot(SUID).Device = "";                 //remove device 
Slot(SUID).Device.ASIO = "Device Name"; //or {GUID} 
Slot(SUID).Device.MME = "Device Name"; 
Slot(SUID).Device.KS = "Device Name"; 
Slot(SUID).Device.WDM = "Device Name";

PresetPatch[i].Apply; 
PresetPatch[i].Comment = "comment" 
PresetPatch[i].Copy; 
PresetPatch[i].Delete; 
PresetPatch[i].Gain = 0.0; 
PresetPatch[i].Load = "FileName" 
PresetPatch[i].Mute = 1 
PresetPatch[i].Name = "Name" 
PresetPatch[i].Paste; 
PresetPatch[i].Phase = 1; 
PresetPatch[i].Recall; 
PresetPatch[i].ResetZone; 
PresetPatch[i].SaveAs = "file name" 
PresetPatch[i].Select; 
PresetPatch[i].Unapply; 
PresetPatch[i].Update

Command.Shutdown 
Command.Show 
Command.Restart 
Command.Reset 
Command.ResetGrid 
Command.Save 
Command.Load 
Command.SaveGrid 
Command.LoadGrid
```

## 请求行指令集（Request Line Instruction Set）

使用疑问标签后，还可以通过一些命令指令从矩阵中获取回复。

示例:
```
Point(ASIO64A.IN[1], ASIO64A.OUT[1]).dBGain = ?;
```

可能回复:
```
Point(ASIO64A.IN[1], ASIO64A.OUT[1]).dBGain = -6;
```

或者
```
Point(ASIO64A.IN[1], ASIO64A.OUT[1]).dBGain = -inf;
```

以下是可用于从矩阵中获取信息的请求列表：

SUID = Slot unique identifier (e.g. ASIO128, VBAN1 etc…).
```
Point(SUID.IN[i], SUID.OUT[j]).dBGain = ?; 
Point(SUID.IN[i1..i2], SUID.OUT[j1..j2]).dBGain = ?;

Point(SUID.IN[i], SUID.OUT[j]).Mute = ?; 
Point(SUID.IN[i1..i2], SUID.OUT[j1..j2]).Mute =?;

Point(SUID.IN[i], SUID.OUT[j]).Phase = ?; 
Point(SUID.IN[i1..i2], SUID.OUT[j1..j2]).Phase =?;

Output(SUID.OUT[j]).Name = ?; 
Output(SUID.OUT[j1..j2]).Name = ?;

Input(SUID.IN[i]).Name = ?; 
Input(SUID.IN[i1..i2]).Name = ?;

Slot(SUID).Online = ?; 
Slot(SUID).Master = ?; 
Slot(SUID).Device = ?; 
Slot(SUID).RunningStatus = ?;           // 0 or 1 
Slot(SUID).Info = ?;                    // ex: "in:4, out:8";

PresetPatch[i].Name = ?; 
PresetPatch[i].Comment = ?; 
PresetPatch[i].Apply = ?;               //number of applied / number max 
PresetPatch[i].Mute = ?;                //number of muted / number max 
PresetPatch[i].Phase = ?;               //number of out of phase / number max 
PresetPatch[i].Gain = ?; 
PresetPatch[i].Zone = ?;                //Number of Zone 
PresetPatch[i].Point = ?;               //Number of Points

Command.Version = ?;                    //app name + version number 
Command.Load = ?;                       //return current file name 
Command.LoadGrid = ?;                   //return current file name 
Command.Engine = ?;                     // returns 0 or 1 + (MASTER SUID, SR, Buffer) 
Command.Master = ?;                     // returns MASTER SUID + (SR, Buffer)
```

# 主按钮（Matrix Main Menu）

点击“左上角”后，用户即可访问各项功能：

![](VBMatrix_UserManual/matrix-14-1.jpg)

附加菜单则用于提供其他功能：

|按钮 |功能 |
|:--|:--|
|**Restart Audio Engine** |重新启动音频引擎。 |
|**Auto Restart Audio Engine(Master Device)** |当主设备断开连接时，自动重启音频引擎。 |
|**Load Settings... <br>Save Settings** |用于以指定文件名加载或保存当前设置。 |
|**Load Settings on Startup** |在启动时加载特定的设置文件，然后以相同的设置重新启动。 |
|**Load Grid Settings only...<br>Save Grid Settings only...<br>Reset Grid Settings only...** |用于加载、保存和重置路由网格设置。 |
|**Reset Settings(Re-Initialization)** |用于重置全部设置。|
|**System Tray** |将 Matrix 置于系统托盘。 |
|**Run on Windows Startup** |随 Windows 系统启动运行。 |
|**Show App On Startup** |在启动时显示 Matrix。 |
|**Set as Always Visible** |将 Matrix 设置为始终可见（置顶窗口）。|
|**Limit Remote Gain to 0 dBfs** |将远程增益（MIDI 控制）限制为 0dB（用以替代 +12dB）。|
|**Log/CLI... <br>Settings... <br>Routings Grid... <br>M.I.D.I. Mapping... <br>VBAN Dialog Box** |用于打开不同的配置对话框（Log/CLI, System settings, Routing Grid, M.I.D.I. mapping, VBAN Dialog Box）|
|**Shut Down Matrix** |关闭 Matrix|

**About Box** 窗口将显示您当前的激活码和许可证状态，并提供相关链接，以便获取更多信息并在线购买许可证。

**System Settings** 对话框允许配置与音频设备管理相关的参数。

**M.I.D.I. Mapping** 对话框允许将 M.I.D.I. 控制器连接到 Matrix。

**VBAN** 对话框将帮助您配置 VB-Audio 网络功能，以便在您的局域网中的任意计算机之间发送或接收音频流。

## 加载设置（Load Settings）

Matrix 设置包含所有设置（仅存储在注册表中的部分系统设置除外）。

- 插槽配置（设备选择、在线/主控状态）。
- Matrix Grid 配置 
    - I/O name 
    - Routing points
- The MIDI mapping 配置
- VBAN 设置

## 仅加载 Grid 设置

Grid 网格设置仅包含以下设置

- Matrix Grid 配置 
    - I/O name 
    - Routing points

## 预设音色（Preset Patch）

预设音色是通过下面 2 项定义的独立路由图

- 矩形区域 (up to 64)
- 区域中的点

这些预设值独立于“设置”或“网格设置”，并永久存储在 `My Documents\VBAudioMatrix\PresetPatch` 文件夹 `(or PresetPatchCoconut)`。

预设补丁提供多个按钮和一个增益滑块（均可进行 MIDI 映射）。

- A：应用预设，应用区域中定义的所有路由（区域中的其他点将被移除）。取消应用预设将移除所有区域点。

- M：静音预设，静音区域内所有点。

- P：相位预设，反转区域内所有点的相位。

- 滑块（SLIDER）：预设增益，相对地调整区域内所有点的增益。

# MATRIX 细节

VB-Audio Matrix 的主界面由多个插槽组成，用于管理不同的音频模块或设备。ASIO 设备和 Windows 设备以插槽形式呈现，选择相应设备后该插槽即被激活；而 VAIO、VBAN 和 VASIO 插槽则需通过“ONLINE”按钮手动激活。

## ASIO SLOT

ASIO 和 WINDOWS 插槽均遵循相同的原则。您可以选择某个设备，该插槽将允许您最多管理指定数量的通道（具体取决于设备的能力）。

ASIO 128 最多可管理一个 ASIO 设备的 128 个输入/输出通道。如果设备提供的通道数超过此上限，则超出部分将被忽略（仅使用前 128 个输入/输出通道）。若 ASIO 设备提供的输入/输出通道数少于插槽的容量，则系统只会考虑实际可用的通道数，例如下文所示的 M‑Audio 设备仅提供 4 个输入/输出通道的情况。

![](VBMatrix_UserManual/matrix-16-1.jpg)

如果输入峰值表中显示有电平，说明 ASIO 设备正在接收信号。如果输出峰值表中显示有电平，说明矩阵正在将某些输入路由至这些输出。输出通道完全由路由网格决定。

## WINDOWS SLOT

WINDOWS 设备插槽与 ASIO 插槽类似，但输入与输出是分开的。其中，WINx.IN 插槽用于选择录音设备（提供输入功能），而 WINx.OUT 插槽则用于选择播放设备（提供输出功能）。WIN 插槽最多可管理 8 个声道；不过，在 Matrix Coconut 上，WIN32 和 WIN64 分别可管理 32 个和 64 个声道（实验性功能）。

此外，WIN 插槽也可作为主设备，但无法与 Windows 录音设备配合使用。主设备（MASTER device）必须非常稳定，并以固定缓冲区大小进行数据流传输；而 Windows 录音设备通常并未以独占模式打开，可能会产生不同的缓冲区大小，从而导致其无法正常作为主设备工作。

![](VBMatrix_UserManual/matrix-17-1.jpg)

以深蓝色显示的采样率或缓冲区大小表示其与主设备的设置不同。不过这并不会影响正常工作，因为矩阵音频引擎能够处理任何以不同采样率或缓冲配置的音频流。

以红色显示的设备名称表示该设备未运行，原因可能是未连接、系统未授权、被其他应用程序占用，或不支持当前的音频格式。

## 查看 I/O 路由

单击峰值表的 I/O 时，显示的路由中会带有非常细小的白色箭头。

![](VBMatrix_UserManual/matrix-17-2.jpg)

单击“输出峰值表（OUT peak meter）”即可查看所有路由至该输出的输入信号。单击“输入峰值表（IN peak meter）”即可查看所有从该输入获取音频的输出信号。

按住 Ctrl 键并单击 I/O 峰值表，即可更改路由设置（无需进入路由网格）。

## WINDOWS 插槽上下文菜单

右键单击以在插槽上打开上下文菜单，并调出设备选择器或 Windows 声音对话框。

![](VBMatrix_UserManual/matrix-18-1.jpg)

## ASIO 插槽上下文菜单

右键单击以在插槽上打开上下文菜单，并调出设备选择器或 Windows 声音对话框。

![](VBMatrix_UserManual/matrix-18-2.jpg)

## VAIO SLOT

虚拟音频输入/输出（Virtual Audio I/O）插槽负责管理通过 Matrix 安装的虚拟输入/输出设备（virtual I/O）。VB-Audio Matrix VAIO 是一款音频驱动程序，可提供最多 8 个输入设备和 8 个输出设备，每个通道又可支持多达 8 个通道。它旨在将任何使用 MME、WASAPI、DirectX 或 KS 音频接口的音频应用程序与音频播放或录制功能相连接。

![](VBMatrix_UserManual/matrix-19-1.jpg)

VAIO 插槽可直接访问此虚拟音频设备。VB-Audio Matrix 使用前 4 个虚拟输入/输出，而 Coconut 版本则可访问全部 8 个虚拟输入/输出。

VB-Audio Matrix 的输入 2、4、6、8 显示为扬声器通道，而输入 1、3、5、7 则显示为线路输出引脚（pin）。扬声器通道配有“CONFIGURE（配置）”按钮，用于选择声道编号：

![](VBMatrix_UserManual/matrix-19-2.jpg)

默认采样率可在属性 -> 高级缩略图中进行定义。

线路输出引脚（Pins）必须通过属性对话框进行配置（此类引脚的“configure（配置）”按钮已被禁用）。

![](VBMatrix_UserManual/matrix-20-1.png)

此对话框中定义的默认格式是应用程序在连接不同设备时所使用的 Windows 音频格式。所有输入/输出均可轻松配置为不同的音频格式、声道数或采样率。Matrix 虚拟音频 I/O 驱动程序（Virtual Audio I/O driver）会自动将其转换为 Matrix 当前使用的格式。

VB-Audio Matrix VAIO 作为 Matrix 应用程序的虚拟 I/O 设备工作：

![](VBMatrix_UserManual/matrix-20-2.jpg)

## VAIO SLOT 上下文菜单

右键单击以在插槽上打开上下文菜单，并启动 VB-Audio Matrix 控制面板。

![](VBMatrix_UserManual/matrix-21-1.jpg)

## VAIO 延迟按钮

<div style="display: grid; grid-template-columns: 4.75fr 0.5fr 4.75fr;">
  <div>
    <p>按住 Ctrl 键并单击“缓冲区大小”，即可打开延迟菜单，从而调整 Matrix VAIO 的内部延迟（输入/输出）。 </p>
    <p>该延迟值由 Matrix 保存在注册表中，并在音频引擎启动时被读取（会覆盖 VAIO 控制面板中可能的设置更改）。 </p>
    <p>7168 样本的延迟设置能够确保 VAIO 在各种情况下均能正常工作，因为它允许连接的应用程序使用最大达 2048 个样本的缓冲区。在这种情况下，要实现稳定的音频流，需要 3 倍的 2048 样本，即 6144 个样本，因此 7168 的设置同样适用。 </p>
    <p>如果在尝试寻找最佳内部延迟时遇到问题（如音频断断续续或完全无声），可以恢复为默认值。 </p>
  </div>
  <div></div>
  <div>

  ![](VBMatrix_UserManual/matrix-21-2.jpg)
  
  </div>
  
</div>

## VBAN SLOT

VB-Audio Matrix 提供 VBAN 插槽，可像 Voicemeeter 一样实现音频在 VBAN 流之间的路由，配备 4 个常规的 VBAN 输入与输出通道（Coconut 版本为 8 个），并首次新增一个 64 通道的 VBAN 输入与输出通道（Coconut 版本额外提供 128 通道的 VBAN 插槽）。

![](VBMatrix_UserManual/matrix-22-1.jpg)

VBAN 服务必须处于开启（ON）状态，且 VBAN 插槽必须设置为在线（Online）才能正常运行。随后，还需在额外的 VBAN 配置对话框中完成 VBAN 流的配置（VBAN 插槽上仅显示“ON（开启）”按钮）。

如果 VBAN 输出流处于关闭（OFF）状态，峰值表可能会显示较暗的电平值，以表明已进行了一些路由设置来为该流提供信号，但并未通过网络发送（即处于关闭状态），如上图所示。

## VBAN 配置

VBAN Configuration dialog box allows to define more precisely each stream, first 4 streams are regular 8 channels VBAN stream, the 5th can be configured (send or received) up to 64 channels.

VBAN 配置对话框允许更精确地定义每个流；前 4 个流为常规的 8 通道 VBAN 流，第 5 个数据流则可配置为发送或接收，最多支持 64 个通道。

![](VBMatrix_UserManual/matrix-22-2.jpg)

Matrix Coconut 提供 10 路 I/O 流，其中第 9 路可支持最多 64 个通道，第 10 路则可支持 128 个通道。

![](VBMatrix_UserManual/matrix-23-1.jpg)

与 Voicemeeter 类似，VBAN 实现提供 MIDI 输入和输出数据流，以及一个 VBAN-TEXT 输入数据流（“Command1”）。

### VBAN 帧（FRAME）

作为最后一项输出流，VB-Matrix 首次推出了 VBAN-Frame 流，支持通过 VBAN-Screen 应用程序实现与另一台计算机的屏幕共享。

![](VBMatrix_UserManual/matrix-24-1.jpg)

它可以捕获整个显示屏（来自4个连接的屏幕，最高4K分辨率）或仅捕获主窗口界面（应用程序视图）。这是通过 VBAN-Frame 协议以每秒最多30次的速度将 PNG 或 JPG 帧发送到目标地址来实现的。

percent 参数用于指定 JPG 的质量。网络质量则是一种理论上的限制，旨在优先保障音频流的传输（默认为 12 Mbps，但并不妨碍设置为 30 Mbps 或更高）。

Screen Sharing and remote control:

如果使用 VBAN-Screen 应用程序来显示由 Matrix 发送的 VBAN-FRAME，那么 Matrix 可以通过 VBAN-TEXT 流接收来自 VBAN-Screen 应用程序的鼠标事件，从而实现远程控制。

![](VBMatrix_UserManual/matrix-24-2.jpg)

为此，请右键单击采样率或格式字段以启用鼠标管理。此时将显示“M”，提示我们正在处理鼠标事件，从而可通过 VBAN-Screen 进行远程控制。

## VASIO SLOT

VASIO 插槽（Virtual ASIO slots）负责管理随 Matrix 一同安装的虚拟 ASIO 驱动程序(virtual ASIO drivers)。VB-Audio Matrix 会安装一组 2×4 的 ASIO 驱动程序，提供多种不同的能力：

VB-Audio Matrix installs 4x virtual ASIO Drivers:

- VASIO8 (8 I/O – 4 client applications) VB-Matrix VASIO-8 
- VASIO128 (8 I/O – 1 client application) VB-Matrix VASIO-128 
- VASIO64A (8 I/O – 2 client applications) VB-Matrix VASIO-64A 
- VASIO64B (8 I/O – 2 client applications) VB-Matrix VASIO-64B

VB-Audio Matrix Coconut installs 4x other virtual ASIO Drivers:

- VASIO256A (256 I/O – 1 client application) VB-Matrix VASIO-256A 
- VASIO256B (256 I/O – 1 client application) VB-Matrix VASIO-256B 
- VASIO32 (32 I/O – 2 client applications) VB-Matrix VASIO-32 
- VASIO512 (512 I/O – 1 client application) VB-Matrix VASIO-512

<div style="display: grid; grid-template-columns: 5fr 0.5fr 4.5fr;">
  <div>
    <p>VB-Matrix 的 ASIO 驱动程序以 32 位和 64 位 DLL 的形式提供，因此可在任何 DAW 应用程序（32 位或 64 位）中使用。</p>
    <p>每个 DLL 都配有对应的图标，分别用于 VB-Audio Matrix 和 Coconut 版本。某些设备选择器可能无法显示相应的图标。</p>
    <p>右侧所示为 Voicemeeter 设备选择器中显示的 ASIO 设备列表。</p>
  </div>
  <div></div>
  <div>

  ![](VBMatrix_UserManual/matrix-25-1.jpg)
  </div>
</div>

# 主时钟与同步（Master Clock and Synchronization）

主时钟为主音频流和音频处理提供参考时间，并确定音频引擎所使用的采样率和缓冲区大小。除虚拟 ASIO、VAIO（根据系统设置选项）以及 VBAN 输出流外，其余音频点在“软”模式下均由主时钟驱动；而这些输出流则以“严格（Strict）”模式运行。

在严格模式（strict mode）下，音频点均严格按照主时钟的频率运行，采用相同的采样率和缓冲区大小。而在软模式（Soft mode）下，音频点则使用各自的时钟运行，且可能具有不同的采样率和缓冲区大小。

为实现处理与同步，所有音频点在必要时都需转换为主时钟的采样率和缓冲区大小。这一同步过程可能会在声音中引入或多或少可闻的失真（尤其对于那些以“软”方式与主时钟同步的音频点）。

![](VBMatrix_UserManual/matrix-26-1.jpg)

**一般建议**是将您首选的音频设备（ASIO 设备或 Windows 输出设备）设置为主设备，这样该音频设备就能与 VAIO、虚拟 ASIO 驱动程序以及 VBAN 输出流实现完美同步（VAIOs 的同步选项需设为“严格模式（STRICT mode）”）。

当系统上未安装音频设备时，或者当您的音频设备可以以不同的采样率运行时，您希望虚拟ASIO驱动程序保持相同的采样率时，内部时钟就变得很有趣。

# EXTRA OPTIONS

> M.I.D.I. Mapping

> Specifications

> Recommendations

> Command line Installation



# 规格参数（Specifications）

## Matrix Specifications

|||
|:--|:--|
|Application Type: |Real Time Audio Matrix, Audio Routing Application |
|Application Compatibility: |Windows XP(SP2), VISTA, WIN7, WIN8, WIN8.1, WIN10/11 (32 / 64 bits + ARM64 compatible) |
|Virtual Audio Driver Compatibility: |Windows 10/11 64 bits + ARM64 <br>(VAIOs not present on other Windows plateform) |
|PC Configuration: |Min: Celeron / Duo Core 1.8 GHz - 512 MB RAM - Disk < 100 MB |
|Audio Engine Capabilities: |44.1, 48, 88.2, 96, 176.4 or 192 kHz DSP Processing (defined by Master Device)|
|Windows Interfaces Capabilities: |WDM, KS, MME, (44.1 kHz to 192 kHz) - 1 to 8 channels |
|Virtual I/O (VAIO): |WDM, KS, MME, Direct-X (8 kHz to 192 kHz) - 1 to 8 channels |
|ASIO Interfaces Capabilities: |ASIO (44.1 kHz to 192 kHz) - 1 to 128 channles. |
|VBAN Implementation: |1x MIDI input stream / 1x TEXT input stream / 5x Audio Streams. |
|VBAN Audio Stream: |5x VBAN Bi-directional Stream (8 channels and 64 channels) |
|M.I.D.I. Implementation (remoting): |- PRESET PATCH selector <br>- PRESET PATCH Apply, Mute, Phase, Gain. <br>- VBAN-TEXT instruction set (see LOG / CLI) |
|Matrix Grid Max: |680 x 680 |
|Matrix Parameters: |Gain from -100 dB (-inf) to +24 dB, Mute, Phase reverse. |
|Matrix Preset: |XML files.|
|Number of Slots: |24. <br>- 3x ASIO Devices. <br>- 4x Windows Input devices. <br>- 4x Windows Output devices. <br>- 4x Windows Virtual I/O devices. <br>- 4x Bi-directional 8 channels VBAN stream. <br>- 1x Bi-directional 64 channels VBAN stream. <br>- 4x Virtual ASIO Driver (8, 64 and 128 channels).|
|Synchronization: |By a selected Master Device or by Internal Clock. <br>(Automatic Sample Rate Conversion if required)|
|Additional functions: |- Talkback / Monitoring. <br>- Log / CLI. <br>- Output Delay by slot.|

## Coconut Specifications

|||
|:--|:--|
|Application Type: |Real Time Audio Matrix, Audio Routing Application |
|Application Compatibility: |Windows XP(SP2), VISTA, WIN7, WIN8, WIN8.1, WIN10/11 (32 / 64 bits + ARM64 compatible) |
|Virtual Audio Driver Compatibility: |Windows 10/11 64 bits + ARM64 <br>(VAIOs not present on other Windows plateform) |
|PC Configuration: |Min: Celeron / Duo Core 1.8 GHz - 512 MB RAM - Disk < 100 MB |
|Audio Engine Capabilities: |44.1, 48, 88.2, 96, 176.4 or 192 kHz DSP Processing (defined by Master Device) |
|Windows Interfaces Capabilities: |WDM, KS, MME, (44.1 kHz to 192 kHz) - 1 to 64 channels |
|Virtual I/O (VAIO): |WDM, KS, MME, Direct-X (8 kHz to 192 kHz) - 1 to 8 channels |
|ASIO Interfaces Capabilities: |ASIO (44.1 kHz to 192 kHz) - 1 to 512 channles. |
|VBAN Implementation: |1x MIDI input stream / 1x TEXT input stream / 10x Audio Streams. |
|VBAN Audio Stream: |10x VBAN Bi-directional Stream (8 channels, 64 and 128 channels) |
|M.I.D.I. Implementation (remoting): |- PRESET PATCH selector <br>- PRESET PATCH Apply, Mute , Phase, Gain. <br>- VBAN-TEXT instruction set (see LOG / CLI) |
|Matrix Grid Max: |3112 x 3112 |
|Matrix Parameters: |Gain from -100 dB (-inf) to +24 dB, Mute, Phase reverse. |
|Matrix Preset: |XML files. |
|Number of Slots: |53. <br>- 7x ASIO Devices (32, 64, 128, 256 and 512 channels). <br>- 10x Windows Input devices. <br>- 10x Windows Output devices. <br>- 8x Windows Virtual I/O devices. <br>- 8x Bi-directional 8 channels VBAN stream. <br>- 2x Bi-directional 64 and 128 channels VBAN stream. <br>- 8x Virtual ASIO Driver (8, 32, 64, 128, 256 and 512 channels). |
|Synchronization: |By a selected Master Device or by Internal Clock. <br>(Automatic Sample Rate Conversion if required) |
|Additional functions: |- Talkback / Monitoring. <br>- Log / CLI. <br>- Output Delay by slot. |

# 建议（RECOMMENDATIONS）

Matrix 已在多个层面通过验证，在大多数配置下使用当前的默认参数时应能正常运行。然而，由于 Matrix 需要兼容多种音频驱动程序、不同的音频接口以及众多不同的音频应用程序（这些应用程序也可能使用不同的音频接口），其复杂性依然较高。因此，要使其在各种环境下稳定协同工作，尤其是在延迟优化方面，可能会面临一定挑战。

## 已知问题（Known issues）

某些 ASIO 应用程序可能会受到我们部分 ASIO 驱动程序中 I/O 数量的影响。例如，ASIO 512 驱动程序提供 1024 个通道，这并不常见，但在专业音频领域已有先例。

## 延迟优化（Latency optimization）

常规的 Windows 系统配置通常难以将缓冲时间控制在 2.5 毫秒以下。这意味着，在12小时或24小时内，音频线程可能会遭遇长达 2.5 毫秒的中断。这一情况可以通过专门的测试应用程序进行测量，例如，您可以在数天内持续运行该程序，以获取最长的中断时长：[https://forum.vb-audio.com/viewtopic.php?t=519](https://forum.vb-audio.com/viewtopic.php?t=519)

2.5 毫秒在 44.1/48kHz 采样率下约等于 128 个样本。因此，128 个样本的缓冲区大小对于 Windows 系统而言已属临界值，难以有效避免音频线程受到中断干扰。若要进一步降低至 128 个样本以下（而我们知道某些 PC 配置甚至可以采用 64 或 48 个样本的缓冲区）则必须依赖经过验证的硬件配置，并可能需要专业的音频技术知识。

## 延迟建议（Latency recommendation）

在 Windows 10 系统下，我们建议将缓冲区大小设置为至少 5 毫秒（在 44.1 kHz 或 48 kHz 采样率下约为 256 个样本），以确保音频流的稳定性。我们所有的默认参数均设为 512 个样本（在 44.1 kHz 或 48 kHz 采样率下约为 10 毫秒），因为我们确信这一缓冲区大小能够为任何 Windows PC 配置提供良好的音频流稳定性。否则，通常表明存在系统、驱动程序或硬件方面的问题。

# Command Line Installation

It is possible to make an automatic installation (or uninstallation) by using command line options. However it will need to reboot after installation (and after uninstallation). So it's recommended to first call the setup program to uninstall possible previous version, then reboot, and then install new version (and reboot again).

```
–h : to hide GUI 
–i : to install 
–u : to uninstall
```

## Matrix Command Line

vbaudiomatrix.exe support some command to restart audio engine or to run Matrix application with a pre-defined configuration file. It allows for example to add different shortcut on the desktop to run Matrix for different jobs.

To Restart Audio Engine by a shortcut use the following command line.
```
vbaudiomatrix.exe –R (or "–r")
```

To run Matrix with a specific configuration file, use these following command lines (Matrix must have been shut down before `– if` Matrix is already running, it will do nothing):
```
–l"filename.xml" or -L"filename.xml"
```

If the xml is in the same directories of voicemeeter.exe 
```
–l"filename.xml" or -L"filename.xml"
```

If the xml is in the same sub directories of VBAudioMatrix.exe 
```
–l"subfolder\filename.xml" or -L"subfolder\filename.xml"
```

Or you can use absolute patch 
```
–l"c:\folder\filename.xml" 
or 
-L"c:\folder\filename.xml"
```

## Registry Parameters

Some parameters in the registry (regedit) can be interesting for some expert users in very specific use case or rare technical problems. Do not modify these values without having getting advice on our support resource (forum, mail).

We are talking here about some values present in the following registry directory 
```
HKEY_CURRENT_USER\VB-Audio\VBAudioMatrix
```

`DelayedStartS`  
This value gives the countdown in second before starting audio engine on Matrix Startup (5 second per default).

`preferredResolution`  
This value gives the preferred bit resolution used by Matrix (24 bits per default).In any cases, the final bit resolution is the result of a negotiation with the audio interface (that can force to use other resolution than the preferred one).

`MaxOutDelayMS`  
500 ms per default to optimize memory allocation, this value gives the maximum delay for output delay options (in the system settings dialog box). It can be redefined by this registry key in millisecond, from 500 ms to 5000 ms (5 seconds max).

**WARNING: Other Registry Values must not be modified directly.**

## AUDIO EXPERT / DEVELOPPERS

`TimerResolution`  
This value can be created and set to '1' to force Matrix to set the system timer resolution to standard 1 ms (instead of 0.5 ms if this value is not set to '1' or not existing).

`EngineMode`  
This value gives a bit field of feature related to WASAPI audio engine. Must be ZERO per default.
```
0x00000001 : MODE_SWIFT 
0x00000100 : INPUT EXCLUSIVE MODE 
0x00000200 : OUTPUT EXCLUSIVE MODE      //set anyway
``` 