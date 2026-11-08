# DISM 命令

```
PS C:\Users\li> dism -?

部署映像服务和管理工具
版本: 10.0.26100.9549


DISM.exe [dism_options] {Imaging_command} [<Imaging_arguments>]
DISM.exe {/Image:<path_to_offline_image> | /Online} [dism_options]
         {servicing_command} [<servicing_arguments>]

描述:

DISM 枚举、安装、卸载、配置和更新 Windows 映像中的功能和程序包。  
可以使用的命令取决于提供的映像以及映像是处于脱机还是运行状态。


FFU 命令:

  /Capture-Ffu            - 将物理磁盘映像捕获到新的 FFU 文件中。
  /Apply-Ffu              - 应用 .ffu 映像。
  /Split-Ffu              - 将现有 .ffu 文件拆分成多个只读已拆分 FFU 文件。
  /Optimize-Ffu           - 优化 FFU 文件，使其其可应用于不同大小的存储。

WIM 命令:

  /Apply-CustomDataImage  - 冻结自定义数据映像中包含的文件。
  /Capture-CustomImage    - 将自定义设置捕获到 WIMBoot 系统上的增量 WIM 文件中。
                            捕获的目录包括所有子文件夹和数据。
  /Get-WIMBootEntry       - 显示指定磁盘卷的 WIMBoot 配置项。
  /Update-WIMBootEntry    - 更新指定磁盘卷的 WIMBoot 配置项。
  /List-Image             - 显示指定映像中的文件和文件夹的列表。
  /Delete-Image           - 从具有多个卷映像的 WIM 文件删除指定的卷映像。
  /Export-Image           - 将指定映像的副本导出到其他文件。
  /Append-Image           - 将其他映像添加到 WIM 文件中。
  /Capture-Image          - 将驱动器的映像捕获到新的 WIM 文件中。
                            捕获的目录包含所有子文件夹和数据。
  /Get-MountedWimInfo     - 显示有关安装的 WIM 映像的信息。
  /Get-WimInfo            - 显示有关 WIM 文件中的映像的信息。
  /Commit-Wim             - 保存对安装的 WIM 映像的更改。
  /Unmount-Wim            - 卸载安装的 WIM 映像。
  /Mount-Wim              - 从 WIM 文件安装映像。
  /Remount-Wim            - 恢复孤立的 WIM 安装目录。
  /Cleanup-Wim            - 删除与损坏的已安装 WIM 映像关联的资源。

通用映像处理命令:

  /Split-Image            - 将现有 .wim 文件拆分为多个只读拆分 WIM (SWM) 文件。
  /Apply-Image            - 应用一个映像。
  /Get-MountedImageInfo   - 显示有关安装的 WIM 和 VHD 映像的信息。
  /Get-ImageInfo          - 显示有关 WIM、VHD 或 FFU 文件中映像的信息。
  /Commit-Image           - 保存对装载的 WIM 或 VHD 映像的更改。
  /Unmount-Image          - 卸载已装载的 WIM 或 VHD 映像。
  /Mount-Image            - 从 WIM 或 VHD 文件装载映像。
  /Remount-Image          - 恢复孤立的映像装载目录。
  /Cleanup-Mountpoints    - 删除与损坏的已安装映像关联的资源。

映像规格:

  /Online                 - 以正在运行的操作系统为目标。
  /Image                  - 指定脱机 Windows 映像的根目录的路径。

DISM 选项:

  /English                - 用英文显示命令行输出。
  /Format                 - 指定报告输出格式。
  /WinDir                 - 指定 Windows 目录的路径。
  /SysDriveDir            - 指定名为 BootMgr 的系统加载程序文件的路径。
  /LogPath                - 指定日志文件路径。
  /LogLevel               - 指定日志(1-4)中所示的输出级别。
  /NoRestart              - 取消自动重新启动和重新启动提示。
  /Quiet                  - 取消除错误消息之外的所有输出。
  /ScratchDir             - 指定暂存目录的路径。

若要获得有关这些 DISM 选项及其参数的详细信息，请在紧挨着 /? 之前指定一个选项。

  示例:
    DISM.exe /Mount-Wim /?
    DISM.exe /ScratchDir /?
    DISM.exe /Image:C:\test\offline /?
    DISM.exe /Online /?


PS C:\Users\li>
```