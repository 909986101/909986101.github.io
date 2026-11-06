# 黑苹果引导

目前常用的黑苹果 bootloader 有 2 个，OpenCore 和 Clover。

不论使用哪一个引导 MacOS 都只需要将下面 2 个目录复制到 `ESP` 分区的 `EFI` 目录下即可。
1. `boot` 目录
1. `OC`（或 `CLOVER`）目录

这就隐含了一个前提条件，因为使用到了 `ESP` 分区，所以磁盘的模式必须是 `GPT`。

## 启动流程

### 加电自检，硬件自举

这里是由主板上的固件 UEFI 来完成的，接着会寻找磁盘启动项（你可以认为在找 ESP 分区）

### bootloader

UEFI 使用 `ESP` 分区中 `/EFI/boot/bootx64.efi` 文件引导计算机。接下来就会使用 `bootloader` 去引导 `MacOS` 系统了。

bootloader
- OC：`/EFI/OC/OpenCore.efi`
- Clover：`/EFI/CLOVER/CLOVERX64.efi`

注意：当 `bootx64.efi` 使用 `OC` 或 `Clover` 引导操作系统时，`OC` 或 `Clover` 会根据 `config.plist` 文件中的设置扫描磁盘，以确定引导哪些操作系统（Windwos、linux 或 MacOS）
  
### kernel

这个阶段是操作系统接管启动了，我们就不用管它了。

## 实践

### 多 ESP 分区

这里的“多”指的是你计算机磁盘上有超过一个 `ESP` 分区。这些分区可以是在同一个磁盘上也可以分散在多个磁盘上。

例如，有三个 `ESP` 分区
1. 第一个分区，用来引导 Windows。如果你有 Windows 系统，那么 `EFI` 分区下会有一个 `Microsoft` 目录。这个是用来引导 Windows 系统的。
2. 第二个分区，使用 OC 来引导。复制 `boot` 目录和 `OC` 目录，到 `EFI` 目录下
3. 第三个分区，使用 Clover 来引导。复制 `boot` 目录和 `CLOVER` 目录，到 `EFI` 目录下

好了，重启你会看到三个引导项，分别是……

### 一个 ESP 分区（Windows + Clover）
   
如果你有 Windows 系统，那么 `EFI` 分区下会有一个 `Microsoft` 目录。不管他。

还是复制 Clover 的 2 个目录到 `EFI` 目录下。接下来用 U 盘引导启动进入 Clover，启动 UEFI Shell，使用 bcfg 命令添加启动项。

### 一个 `ESP` 分区（Windows + OC）

类似 Clover。