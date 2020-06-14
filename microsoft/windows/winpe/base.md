# WinPE 基础

## 创建可启动 WinPE 介质

>https://docs.microsoft.com/zh-cn/windows-hardware/manufacture/desktop/winpe-create-usb-bootable-drive

### 步骤一：创建工作文件

1. 以管理员身份启动“部署和映像工具环境”

1. 运行“copype”以创建 Windows PE 文件的工作副本

       copype amd64 C:\WinPE_amd64

### 步骤二：自定义 WinPE（可选）

略

### 步骤三：创建可启动介质

#### 方法一：创建可启动的 WinPE U 盘

1. 以管理员身份启动“部署和映像工具环境”

1. 使用 MakeWinPEMedia 以 /UFD 选项格式化 U 盘并安装 Windows PE 到 U 盘

       MakeWinPEMedia /UFD C:\WinPE_amd64 P:

#### 方法二：使用多个分区 USB 驱动器

>https://docs.microsoft.com/zh-cn/windows-hardware/manufacture/desktop/winpe--use-a-single-usb-key-for-winpe-and-a-wim-file---wim#create-two-partition-drive

MakeWinPEMedia 会将 WinPE 驱动器格式化为 FAT32。 如果希望能够在 WinPE U 盘上存储大于 4GB 的文件，则可以创建多分区 U 盘，其具有一个附加分区，格式为 NTFS。

1. 以管理员身份启动“部署和映像工具环境”

1. 键入 **diskpart** 并按 Enter

1. 使用 Diskpart 重新格式化驱动器，并为 WinPE 和映像创建两个新分区

       List disk
       select disk X    (where X is your USB drive)
       clean
       create partition primary size=2048
       active
       format fs=FAT32 quick label="WinPE"
       assign letter=P
       create partition primary
       format fs=NTFS quick label="Images"
       assign letter=I  
       Exit

1. 将 WinPE 文件复制到 WinPE 分区

       copype amd64 C:\WinPE_amd64
       xcopy C:\WinPE_amd64\media P:\ /s

1. 将 Windows 映像文件复制到 Images 分区

       xcopy C:\Images\install.wim I:\install.wim

## 装载、卸载

### 装载 Windows PE 启动映像

- 使用 DISM 将 WinPE 映像装载到某个临时位置

      Dism /Mount-Image /ImageFile:"C:\WinPE_amd64\media\sources\boot.wim" /index:1 /MountDir:"C:\WinPE_amd64\mount"

### 卸载 Windows PE 映像并创建媒体

- 卸载 WinPE 映像并提交更改

      Dism /Unmount-Image /MountDir:"C:\WinPE_amd64\mount" /commit

### 故障排除

**删除工作目录**

在某些情况下，你可能无法恢复装载的映像。DISM 可以防止意外删除工作目录，因此，你可能需要尝试以下步骤才能着手删除装载的目录。尝试以下每个步骤

1. 尝试重新装载映像

       dism /Remount-Image /MountDir:C:\mount

1. 尝试卸载映像并丢弃更改

       dism /Unmount-Image /MountDir:C:\mount /discard

1. 尝试清理与已装载映像关联的资源

       dism /Cleanup-Mountpoints