# VB-AUDIO CABLE 参考手册

以虚拟音频线缆形式工作的虚拟音频设备

![](../_media/cable-1-1.jpg)

# 引言

VB-CABLE 是一款 Windows 音频驱动程序（无需硬件），被称为虚拟音频驱动，其工作原理类似于一根简单的虚拟音频线缆，可将音频信号从输入端传输至输出端。由此，它能够实现两个应用程序之间的连接，例如将播放器应用程序与录音应用程序相连接。

VB-CABLE 在系统中与其他音频设备无异，它会以播放和录制点的形式呈现所有音频接口：MME、WASAPI、KS 和 Direct X。

<div style="display: grid; grid-template-columns: 10fr 0.5fr 10fr;">
  <div>

  ![](../_media/cable-3-1.jpg)
    <p>播放设备（CABLE 输入端）可像扬声器一样配置为不同模式（从单声道到7.1声道的家庭影院设置），并支持 44.1 kHz 至 96 kHz 或 192 kHz 的采样率（16 位或 24 位解析度）。
    </p>
    <p>与常规音频设备一样，CABLE 输入端可设置为系统首选/默认设备，并可同时被多个客户端应用程序使用。
    </p>
  </div>
  <div>
  </div>
  <div>

  ![](../_media/cable-3-2.jpg)
    <p>录音设备（CABLE 输出端）也可通过属性对话框进行配置，支持 44.1 kHz 至 96 kHz 或 192 kHz 的采样率（16 位或 24 位解析度）。
    </p>
    <p>CABLE 输出端仅用于传输来自另一端（CABLE 输入端）的信号。
    </p>
  </div>
</div>

## 最简单的虚拟音频线缆

VB-CABLE 是最简单的虚拟音频线缆，因为它可以接受所有音频格式作为输入，并在需要时自动进行转换以输出。换言之，VB-CABLE 有望在任何场景下都能工作，无需进行配置。播放器应用程序可以以任何音频格式（16 位或 24 位，44.1 至 192 kHz，1 至 8 个通道）向 CABLE 输入端发送音频，而录音机应用程序也可以从 CABLE 输出端以任何其他音频格式捕获音频。

# 安装 VB-Cable 

VB-CABLE 可安装在从 XP SP2 到最新 Win11 32 位或 64 位的所有 Windows 系统上。对于 Win10/11 Arm64，安装程序将自动为您当前的操作系统安装正确的驱动程序。

**步骤1**：将压缩文件中的所有文件解压到一个临时的本地文件夹（位于系统盘）中。由于安装程序需要访问所有未压缩的文件，因此无法直接从压缩包中启动。

**步骤2**：在管理员模式下运行安装程序（右键点击 exe 文件以获取菜单）：
- 适用于64位操作系统：VBCABLE_Setup_x64.exe 
- 适用于32位操作系统：VBCABLE_Setup.exe 

**步骤3**：按照指示操作并等待流程结束。安装完成后请重启计算机（卸载后同样需要重启）。

![](../_media/cable-4-1.jpg)

# 卸载 VB-Cable

如果 VB-CABLE 已经安装，安装程序会提示您删除驱动程序（而不是安装它）。

![](../_media/cable-5-1.jpg)

完成后，别忘了重启电脑，以便 Windows 完成卸载程序。如果重启后驱动程序仍未被移除，你将需要通过 Windows 设备管理器手动删除它：

![](../_media/cable-5-2.jpg)

# 将 VB-Cable 设置为默认设备

安装完成后，您可以设置或检查默认音频设备。在 Windows 10 及更高版本中，最后安装的音频驱动程序可能会自动设置为默认设备，而这可能并非您所愿。

<div style="display: grid; grid-template-columns: 10fr 0.5fr 10fr;">
  <div style="grid-column: 1; grid-row: 1;">
    <p>所有电脑声音将进入 VB-CABLE 输入端（因此您将听不到任何声音）。</p>
  </div>
  <div style="grid-column: 1; grid-row: 2;">

  ![](../_media/cable-6-1.jpg)
  </div>
  <div style="grid-column: 1; grid-row: 3;">
    <p>默认播放设备也可以在 Windows 的“声音”对话框（“播放”选项卡）中设置。</p>
  </div>
  <div style="grid-column: 1; grid-row: 4;">

  ![](../_media/cable-6-3.jpg)
  </div>
  <div style="grid-column: 2; grid-row: 1 / span 4;">
  </div>
  <div style="grid-column: 3; grid-row: 1;">
    <p>您的默认麦克风将设置为 VB-CABLE 输出端（因此，所有音频均将传输至 VB-CABLE 输入端）。</p>
  </div>
  <div style="grid-column: 3; grid-row: 2;">

  ![](../_media/cable-6-2.jpg)
  </div>
  <div style="grid-column: 3; grid-row: 3;">
    <p>在 Windows 的“声音”对话框（“录制”选项卡）中，可以选择默认的录音设备</p>
  </div>
  <div style="grid-column: 3; grid-row: 4;">

  ![](../_media/cable-6-4.jpg)
  </div>
</div>

VB-CABLE for Win10/11 x64/Arm64 installs 2x different inputs. The first is a speaker playback device (that can be setup with configure button) limited to 8 channel (7.1 speaker config). The Second CABLE input is a Line Out pin able to manage up to 16 channels. Both are setup in stereo 48 kHz by default.

适用于 Win10/11 x64/Arm64 的 VB-CABLE 安装了 2 个不同的输入设备。第一个是扬声器播放设备（可通过“配置”按钮进行设置），限制为 8 声道（7.1 扬声器配置）。第二个 CABLE 输入是线路输出引脚，最多可管理 16 声道。默认情况下，这两个设备均设置为立体声 48 kHz。

# 设置 VB-Cable 音频格式

The VB-CABLE default format is stereo 48 kHz (for Win10/11) and stereo 44.1 kHz for previous version. The VB-CABLE input or output format can be changed by application connected to it, but most of applications are using the current defined format. So it can be useful to change the audio format, especially the number of channels and the sample rate if needed.

For "Speaker" pin, the channel number can be configured by the **configure** button.

VB-CABLE 的默认格式为立体声 48 kHz（适用于 Windows 10/11）和立体声 44.1 kHz（适用于早期版本）。VB-CABLE 的输入或输出格式可通过与其连接的应用程序进行更改，但大多数应用程序都使用当前定义的格式。因此，如有需要，更改音频格式，尤其是声道数量和采样率，可能会很有用。

对于“Speaker”引脚，可以通过“**配置**”按钮配置通道号。

![](../_media/cable-7-1.jpg)

对于“线路输出”插孔，必须在“高级”属性中以默认音频格式定义通道数量（两个 cable 输入不能同时使用）：

![](../_media/cable-7-2.jpg)

VB-CABLE 录音设备是一个“线路输入”引脚，因此必须在“高级”属性中定义默认音频格式下的通道数量：

![](../_media/cable-8-1.jpg)

VB-CABLE 早期版本（XP 到 Win7）仅支持 8 个通道。这 8 个通道也存在于 VB-CABLE 输出（录音设备）中，但仅在 XP 下可通过 MME 使用。自 Vista 起，MME 仅支持立体声。不过，通过 KS 接口，这 8 个通道仍然可用。WIN10/11 版本为所有接口（MME、WASAPI、KS）提供 8 个通道（或最多 16 个）。

REM：VB-Audio Matrix coconut 能够管理提供超过 8 个通道（最多 64 个通道）的 Windows 音频设备。

# VB-Cable 控制面板

VB-Cable 控制面板应用程序可以在ZIP压缩包或安装文件夹中找到：

![](../_media/cable-9-1.jpg)

VB-CABLE 控制面板主要用于在某些特定情况下提供帮助，或用于改善音频质量或实时流媒体方面。VB-CABLE 控制面板允许设置两个重要的系统参数：**Max Latency（最大延迟）**（pipe size（管道大小））和 **internal sample rate（内部采样率）**（称为“Internal SR（内部采样率）”）。

![](../_media/cable-9-2.jpg)

VB-CABLE 控制面板显示当前系统参数（左上角）：

- **Driver Name:** VB-Audio Virtual Cable
- **Driver Version:** 3.3.1.7
- **Max Latency:** 7168 (驱动程序初始化时分配的最大内存)
- **Internal SR:** 48000 Hz (the working samplerate of the cable)
- **Latency:** 7168 (可以即时更改以改善延迟)

Input / Output 当前设置显示当前 Windows 音频格式配置或已连接客户端应用程序所使用的音频格式（应用程序可能会根据操作系统版本和所使用的音频接口类型来设置/更改输入/输出格式）。

- **S0, S1**... 数字或系统流已连接
- **L** : 回环使用中

VB-CABLE 控制面板还显示与缓冲相关的统计数据，有助于优化延迟。这些统计数据是针对不同缓冲区大小的简单计数器：

b128 = 缓冲区数量大于或等于 128 个样本 = nb buffers < 256 samples.  
b256 = 缓冲区数量大于或等于 256 个样本 = nb buffers < 512 samples.  
b512 = 缓冲区数量大于或等于 512 个样本 = nb buffers < 1024 samples.

操作系统可以为流式音频使用不同的缓冲区大小。在上图中，我们可以看到，cable input（电缆输入）（一种音频播放设备）被分配了 128 个样本的缓冲区，以及 256、512 或 1024 个样本的缓冲区。准确地说，这些统计数据意味着 VB-CABLE 接收到的缓冲区大小在 128 至 1024 个样本以上之间。

Input driver info（输入驱动信息）和 Output driver info（输出驱动信息）是用于调试的。Error DMA F/H 必须为 0 / 0。

## 配置内部采样率

VB-CABLE 在内部工作时采用固定的采样率（由内部采样率指定）。它允许（独立地）管理输入端和输出端上的任何音频采样率格式。这样，一个 DVD 播放器可以在 VB-CABLE 输入端上发送 48 kHz的声音，而另一个音频应用程序则可以在 VB-CABLE 输出端上以 44.1 kHz的采样率进行录制。转换过程由 VB-CABLE 自动完成。

<div style="display: grid; grid-template-columns: 3.5fr 0.5fr 5fr;">
  <div>
  
  ![](../_media/cable-11-1.jpg)
  </div>
  <div></div>
  <div>
    <p>主菜单允许设置不同的选项。</p>
    <p>7168 作为默认缓冲区大小，通常足以满足任何常规工作流程的需求，因为如果连接的应用程序使用的缓冲区大小低于 2048 个样本，它能保证稳定的流。然而，对于高采样率用例（例如 192 kHz）而言，这可能就不够用了。
    </p>
    <p>“Set Max Latency: 32768 smp...”该菜单允许在驱动程序初始化时分配更多内存，以便能够使用更大的内部延迟。
    </p>
    <p>内部采样率可以动态更改，但若要使其持久（存储在注册表中），控制面板必须在管理员模式下运行。
    </p>
  </div>
</div>

VB-CABLE（Win10/11 版）支持输入/输出采样率为 8 kHz 至 192 kHz，而标准内部采样率为 44.1、48、88.2、96、176.4 和 192 kHz。

如果输入/输出的采样率与内部采样率相同，声音将直接通过线缆传输，无需转换，从而获得最佳的音频质量！这就是为什么在特定使用场景下设置正确的内部采样率会很有用。

但是，根据客户端应用程序使用的 Windows 版本和音频接口（如MME、WASAPI、DX），系统组件（如 kMixer）可以进行所需的转换并降低音质（与 VB-CABLE 无关）。

![](../_media/cable-11-2.jpg)

例如，在 Windows 7 中，转换是在 Windows Media Player 进行的，而在 Windows XP 中，VB-Cable 输入采样率会发生变化。

## 配置内部延迟

VB-CABLE can now let you change the latency on the fly or by editing the value on main view, or by using the latency menu.

VB-CABLE 现在允许您实时更改延迟，或在主视图中编辑值，或使用 **Latency（延迟）**菜单进行更改。

![](../_media/cable-12-1.jpg)

如果根据统计数据（连接到 cable 的应用程序使用的缓冲区）认为延迟过小，计数器会变为红色，声音可能会中断或完全静音。

![](../_media/cable-12-2.jpg)

只需输入一个更大的值，直到红色显示消失

![](../_media/cable-12-3.jpg)

## 回环流式传输

微软 Windows 提供了 WASAPI 接口，用于捕获播放设备的音频流（而不仅仅是录音设备）。这一功能旨在让远程处理程序能够捕获播放的声音。此前的音频流由系统管理，但现在是新的 Win10 驱动程序架构中的一项特殊功能，必须在驱动程序级别进行管理。默认情况下，环回选项处于激活状态，允许您捕获 VB-CABLE Input。

![](../_media/cable-13-1.jpg)

## Windows 音量控制

新版本的 VB-CABLE 通过选项实现了 Windows 音量控制，使您可以使用常规的 Windows 控制器来更改 VB-CABLE 输入（播放设备）的音量。否则，音量控制无效（静音控制可能有效，具体取决于 Windows 版本）。

![](../_media/cable-13-2.jpg)

## 重置插孔名称和图标

将允许您重置 VB-CABLE 设备的图标和 pin 名称（在管理员模式下运行 VB-CABLE 控制面板）。

## 理解延迟

VB-CABLE 基本上需要 3 个缓冲区来形成连续的音频流（一个用于输入，一个用于内部，一个用于输出），设置最大延迟的难度取决于操作系统，操作系统会使用不同的缓冲区大小来传输音频。

<div style="text-align: center;">
  <h1>Max Latency = 3 x Max Buffer Size</h1>
</div>

**Statistics：**旨在让您合理定义电缆的最佳最大延迟，并首先找到当前音频流使用的最大缓冲区大小。这意味着您需要通过 cable（使用播放器应用程序和录音机应用程序）播放流媒体，用来在设置 VB-Cable 最大延迟之前分析统计数据。



<span style="color:red;">重要的是要理解，音频流缓冲取决于客户端应用程序以及这些应用程序所使用的音频接口（MME、KS、WASAPI 的行为各不相同）。如果你为使用 KS 音频接口的 DVD 播放器和 Audacity 设置了最佳延迟，那么它可能就无法再与其他播放器和录音应用程序一起使用了。
</span>

<div style="display: grid; grid-template-columns: 3.5fr 0.5fr 5fr;">
  <div>
  
  ![](../_media/cable-14-1.jpg)
  </div>
  <div></div>
  <div>
    <strong>查找最大缓冲区大小：</strong>
    <p>根据左边的统计数据，音频流使用的缓冲区大小从未超过或等于512个样本。
    </p>
    <p>因此，此流应使用 512 个样本的缓冲区。512 可视为当前音频流使用的最大缓冲区大小。
    </p>
    <p>So MAX Latency = 3 x 512 = 1536</p>
    <strong style="color: red;">只有当输入/输出与内部采样率配置相同时，此结果才成立。
    </strong>
  </div>
</div>

这一基本公式同样适用于 Hi-Fi Cable。然而，对于 VB-CABLE 而言，由于其内部采样率可能与输入和输出采样率不同，因此最佳最大延迟需按以下比例进行缩放：InternalSR / (i/o SR)。

$$
Max \ Latency = 3 \times (Max \ Buffer \ Size) \times \frac{InternalSR}{OutputSR}
$$

在上述示例中，如果内部采样率为 96 kHz，而输入/输出采样率为 44.1 kHz，则我们的最大延迟需按 96/44.1 进行缩放。

$$
Max \ Latency = 3 \times 512 \times \frac{96000}{44100} = 1536 \times 2.177 = 3343
$$

因此，在这种情况下，真正的最大延迟必须设置为至少 3343 个采样点（建议值为 4096）。

## 在特定情况下寻找最优延迟

用于计算最优最大延迟的一般公式要复杂得多，需要在控制面板中以建议形式供用户参考……不过，我们仍可根据统计结果对各种可能情形进行分析。

**始终采用统计给出的最大缓冲区大小：**

<div style="display: grid; grid-template-columns: 3.5fr 0.5fr 5fr;">
  <div>
  
  ![](../_media/cable-15-1.jpg)
  </div>
  <div></div>
  <div>
    <p>据统计，音频源应用程序的音频流使用最大缓冲区大小为 512 个采样点，而音频录制应用程序的音频流则使用最大缓冲区大小为 1024 个采样点。
    </p>
    <p>取两者中的较大值，并据此计算最大延迟：3 × 1024（× 采样率缩放因子）
    </p>
  </div>
</div>

**重要说明：** 只要 VB-CABLE 的当前延迟等于或高于根据统计计算出的最高延迟，它就能正常工作（这也是为何默认值设为 7×1024 或 8×1024 个采样点的原因。在大多数情况下，这一数值足以应对高达 96 kHz 的音频流）。然而，如果当前的最高延迟低于统计计算所得的最高延迟，则可能会出现音频断续（即流的连续性问题）。

**如果统计信息过载，请使用最大延迟：**

<div style="display: grid; grid-template-columns: 3.5fr 0.5fr 5fr;">
  <div>
  
  ![](../_media/cable-15-2.jpg)
  </div>
  <div></div>
  <div>
    <p>如果流式传输使用的是 1024 样本的缓冲区或更大，您就必须考虑采用最大延迟模式，尽管尚无法确定其是否能正常工作（因为流式传输也可能使用 2048 或 8192 的缓冲区，而我们在此处无法观察到，因为统计信息仅限于 1024 样本的缓冲区大小）。
    </p>
  </div>
</div>

注意：对于 VB-CABLE，您可以降低内部采样率以增大有效管道尺寸（pipe size）。

**Hi-Fi Cable 上的统计:**

<div style="display: grid; grid-template-columns: 3.5fr 0.5fr 5fr;">
  <div>
  
  ![](../_media/cable-15-3.jpg)
  </div>
  <div></div>
  <div>
    <p>Hi-Fi Cable 的统计数据支持高达 2048 的缓冲，因为这样可以支持更高的采样率，而音频流通常会随着采样率的提高而增加缓冲。
    </p>
  </div>
</div>

REM：当客户端音频应用程序使用 KS 或 WASAPI 音频接口时，VB-CABLE 通常会接收相同的缓冲区大小。上文中的情况就是如此，输入时只有 b512 计数器增加（因为音频声音是通过 KS 接口以 512 个样本缓冲区发送的），而 MME 缓冲则可以使用各种缓冲区大小来管理音频流（正如我们在输出统计数据（右列）中所见）。因此，如果您确定您的音频应用程序是如何缓冲音频流的，则可以使用它来配置最大延迟（无需使用统计数据 —— 或仅用于检查设置的一致性）。

# Hi-Fi Cable 和 ASIO Bridge

HiFi Cable 与原版 VB-CABLE 略有不同，因为它不包含 SRC（采样率转换器）。因此，只有在输入输出端配置了相同的采样率时，它才能正常工作。

![](../_media/cable-16-1.jpg)

HiFi Cable 控制面板被称为 **ASIO Bridge**，因为它支持将虚拟输入/输出路由到 ASIO 设备。默认情况下，HiFi Cable 处于 **Pass Through（直通）** 模式：常规模式，即输入端所有音频信号都会直接输出到 HiFi Cable 的音频输出端。在 **ASIO Direct（直接）** 模式下，HiFi Cable 输入端会被路由到 ASIO 输出端，而 ASIO 输入端则会被路由到 HiFi Cable 输出端。从某种程度上说，ASIO Bridge 是一种音频接口转换器，它允许音频应用程序通过其常规音频管理（MME、KS、Direct-X或WASAPI）来使用 ASIO 设备。

注意：如果未启动 ASIO Bridge 应用程序，Hi-Fi Cable 仍会以直通模式工作。

## HiFi Cable 最大延迟

由于支持高达 384 kHz 的音频流，Hi-Fi Cable 提供了更多选项来设置最大延迟时间（最高可达32,000 个采样点）。

![](../_media/cable-16-2.jpg)

## 当最大延迟不足时发出警报

HiFi Cable 控制面板每秒进行一次统计分析，以判断管道带宽是否足以支撑各输入/输出流所使用的缓冲。若当前的最大延迟过低，LCD 下方将显示闪烁的提示文字，建议调整新的最大延迟值。

![](../_media/cable-17-1.jpg)

当当前电缆延迟过小，无法支持当前音频流时，液晶屏下方会显示红色文字。

## 当 ASIO 缓冲区过大时发出警告

如果 ASIO 缓冲区大小相对于线缆的最大延迟（Cable MAX Latency）过大，系统将以红色闪烁矩形显示该值。同样，我们仍需遵循主要规则：所使用的缓冲区大小不得超过线缆最大延迟的三分之一。

![](../_media/cable-17-2.jpg)

## 当采样率不同时发出警告

由于 Hi-Fi Cable 不内置采样率转换器，因此所有音频的采样率必须保持一致，才能确保不同音频流正常工作。这些显示的采样率仅在使用 ASIO Bridge 对话框时才会闪烁；这意味着只有当有应用程序连接到虚拟音频输入或输出端口时，才会出现这一现象。

注：当然，如果采样率闪烁，很可能表明音频流已损坏，因为其并未以正确的采样率运行。

## 当 ASIO 驱动未启动时发出警告

如果 ASIO 驱动程序未启动，设备名称后会显示（已停止）。要重新启动它，请在弹出菜单中再次选择 ASIO 设备，或切换两次 ASIO Bridge 模式（PASS Through 和 ASIO Direct）。

![](../_media/cable-18-1.jpg)

## ASIO 时钟异常警报

ASIO Bridge 包含一项采样率测量，用于检测 ASIO 驱动程序实际输出的采样率。此举旨在识别硬件配置错误，例如同步模式不当、字时钟设置错误，以及任何默认时钟设置异常等情况。

常见问题往往源于硬件输入端采用的采样率与软件要求不一致。例如，当播放一张标称采样率为 48 kHz 的 DVD 时，ASIO 驱动程序可能以该设置启动，但最终却以 44.1 kHz 运行，这是因为数模转换器或音频物理连接由另一套时钟信号所驱动所致。

![](../_media/cable-18-2.jpg)

如果存在 ASIO 时钟问题，测得的采样率（此处为 44100 Hz）将显示在一个闪烁的红色矩形中。

# VB-CABLE Under WINDOWS XP

# 在 Windows XP 下安装 VB-CABLE

VB CABLE 是一款标准的 MME / KS / Direct X 音频驱动程序，提供播放与录音接口（与其他普通音频设备完全相同）。安装时，只需将压缩包解压至本地磁盘上的任意文件夹，并运行 **VBCABLE_Setup.exe** 程序（适用于 32 位操作系统）。

<div style="display: grid; grid-template-columns: 15fr 1fr 14fr;">
  <div>
  
  ![](../_media/cable-20-1.jpg)
  </div>
  <div></div>
  <div>
    <p>安装程序：</p>

  ![](../_media/cable-20-2.jpg)
    <p>仍要继续安装驱动程序：</p>

  ![](../_media/cable-20-3.jpg)
  </div>
</div>

安装完成后，您可以在“控制面板”/“声音和音频属性”对话框中查看系统是否已成功安装新的音频设备，该设备名为 **VB-Audio Point**。

REM：（在VISTA以上版本的其他操作系统中，驱动程序名称为 VB-CABLE input/output）。

## 将 VB-CABLE 选为默认设备

VB-CABLE 的工作方式与普通音频设备无异，任何支持 MME、KS 或 Direct-X 音频接口的音频应用程序均可将其设为播放设备。

<div style="display: grid; grid-template-columns: 15fr 1fr 14fr;">
  <div>
    <p>要录制计算机上播放的任何声音，请将 VB-AUDIO CABLE 选为默认播放设备。此后，计算机上播放的每一项音频都将被发送到 VB-CABLE 输入端。
    </p>
    <p>警告：在 VB-CABLE 输出端未路由至物理声卡输出（通过其他音频应用程序）之前，您的扬声器将不再发出任何声音。
    </p>
    <p>提示：请别忘了点击“应用”按钮以确认您的选择。
    </p>
  </div>
  <div></div>
  <div>

  ![](../_media/cable-21-1.jpg)
  </div>
</div>

然后，您可以启动一个播放器应用程序（使用默认的播放设备）。例如 VLC、Windows Media Player、Winamp 等。

![](../_media/cable-21-2.jpg)

检查声音是否已输入到 VB-Cable 输入端

VB-CABLE 软件包中附带了一个小型的控制面板程序，可用于检测其是否正常工作。

![](../_media/cable-22-1.jpg)

在这里，您可以在输入电平（input levels）部分查看音频信号是否来自 cable input（播放设备）。您可以单击该选项以切换电平单位（dB 或 % 电平）。

输入与输出部分显示了音频端点配置（播放与录音设备的音频端点）。在 Windows XP 系统下，该配置由客户端应用程序进行设置。上图中未显示输出配置，是因为当前没有客户端应用程序连接到该端点（录音设备）。请注意，VB-CABLE 能够在两个端点上实时处理任何格式变化，用户无需进行任何配置。

统计数据用于分析目的（面向高级用户）。

## 使用 Audacity 监控 VB-CABLE 输出

Audacity® 是一款免费、开源、跨平台的音频录制与编辑软件。 (http://audacity.sourceforge.net/).

首先，您可以将 Audacity 的设备设置为录制来自 VB-CABLE 输出的信号，并将其通过实际的音频输出（在本例中为 Realtek HD Audio 输出）进行播放。

![](../_media/cable-23-1.jpg)

您可以通过使用“START MONITOR（启动监听）”功能来确认信号确实来自 VB-CABLE。随后，您将看到电平表随之变化。

![](../_media/cable-23-2.jpg)

## 使用 Audacity 录制 VB-CABLE 输出

只需按下“RECORD（录制）”按钮。

![](../_media/cable-24-1.jpg)

来自 VB-CABLE 的声音会被录制，随后可通过真实的音频输出设备进行回放（只需点击“PLAY（播放）”即可）。

路由图：

![](../_media/cable-24-2.jpg)

由于 VB-CABLE Input 已被设置为默认的播放音频设备，因此所有播放器都会将声音发送给它。随后，录音应用程序便可从 CABLE-Output 这一虚拟录音音频设备中捕获信号。

## VB-CABLE 控制面板

本应用程序随驱动程序包一同提供，可用于查看驱动程序的状态，包括版本、配置以及用于诊断与调试的特定数据。旧版的 VB-CABLE 控制面板在选项与功能方面较为有限（例如，相较于 2024 年最新版）。

![](../_media/cable-25-1.jpg)

VB-CABLE 在内部以固定采样率和固定管道大小（默认为 7168 个样本）运行，并支持 8 kHz 至 96 kHz 的 I/O 采样率范围。

**Input Levels** 显示每个可能输入通道的输入信号电平。

**Input and output** 配置（声道数、采样率、分辨率）展示了当前驱动程序的引脚配置，该配置取决于操作系统以及使用该驱动程序的应用程序。

**Statistics** 提供与内部管道相关的各类数据：缓冲区计数、输入端丢失的缓冲区（推送丢失）或输出端丢失的缓冲区（拉取丢失）。其中 bxxx 值表示缓冲类型：即客户端应用程序如何向输入设备提供数据并获取输出信号（在本例中，信号通过小于 512 个样本的缓冲区进行传输）。

**Latency:** VB-CABLE 输入与输出之间的最大延迟由管道大小决定，默认为 7168 个样本。这一数值经过精心选择，以便使虚拟电缆能够兼容大多数客户端应用程序，并允许最多 2048 个样本的缓冲。

# VB-CABLE 定制化

VB-CABLE 音频设备允许您重新定义引脚名称和图标（通过属性对话框）。

![](../_media/cable-26-1.jpg)

但只有最新版本的 Windows 10/11 才能让你修改该设置并使其持久生效。此前的 VB-CABLE 版本（适用于 XP 至 Windows 7）在 Windows 启动时可能会重置图标和固定名称。

![](../_media/cable-26-2.jpg)

REM：驱动程序名称不可更改。
