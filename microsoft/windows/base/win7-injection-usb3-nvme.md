# Windows 7 注入 USB3.0 和 NVMe

Windows7 安装镜像注入 USB3.0 和 NVMe 驱动，支持 UEFI 启动

## 一、制作前的准备

1. 系统环境以 Windows 7 SP1 x64 为例，首先需要下载 MSDN 原版镜像。

    镜像地址：cn_windows_7_ultimate_with_sp1_x64_dvd_u_677408.iso

2. Windows AIK 自动部署工具，可以到网上下载独立版，也可以到微软官方网站下载完整版。

    下载地址：https://www.microsoft.com/zh-cn/download/details.aspx?id=5753

3. 驱动：驱动一般到制造厂商官网上面都有下载，注意选择适合 Windows 7 SP1 64 位版本的驱动。

4. 补丁：微软推出了适用于 Windows 7 的 Nvme 固态硬盘通用驱动  KB2990941-v3 和 KB3087873-v2 。

## 二、开始制作

1. 以 D 盘为例，在 D 盘根目录下建立文件夹 mkos，mkos 下分别建立drivers、hotfix、mount、os、winremount 五个文件夹，其中 drivers 和 hotfix 分别存放驱动程序和补丁。

2. 解压 MSDN 下载的原版系统镜像所有文件到 os 文件夹。

3. 对安装环境 boot.wim 加入驱动和补丁

   - 首先对索引 1 进行操作，在 cmd 命令提示符下，依次输入

         dism /Mount-Wim /WimFile:D:\mkos\os\sources\boot.wim /index:1 /MountDir:D:\mkos\mount
         dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\x64
         dism /Image:D:\mkos\mount /Add-Driver /Driver:D:\mkos\drivers /Recurse /Forceunsigned
         dism /UnMount-Wim /MountDir:D:\mkos\mount /Commit

   - 然后对索引 2 进行同样的操作：

         dism /Mount-Wim /WimFile:D:\mkos\os\sources\boot.wim /index:2 /MountDir:D:\mkos\mount
         dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\x64
         dism /Image:D:\mkos\mount /Add-Driver /Driver:D:\mkos\drivers /Recurse /Forceunsigned

   - 现在先别急着保存卸载镜像，还有一部很重要的工作要做，打开 D:\mkos\mount\sources 文件夹，按修改时间排列文件，然后选中所有刚刚修改的文件，复制到 D:\mkos\os\sources 文件夹下并替换同名文件，保存并卸载镜像。

         dism /UnMount-Wim /MountDir:D:\mkos\mount /Commit

    至此，完成对安装环境boot.wim的操作。

4. 对系统映像 install.wim 加入驱动和补丁

   - 索引 1：

         dism /Mount-WIM /WimFile:D:\mkos\os\sources\install.wim /Index:1 /MountDir:D:\mkos\mount
         dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\all
         dism /Image:D:\mkos\mount /Add-Driver /Driver:D:\mkos\drivers /Recurse /ForceUnsigned
         dism /Mount-WIM /WimFile:D:\mkos\mount\windows\system32\recovery\winre.wim /Index:1 /MountDir:D:\mkos\winremount
         dism /Image:D:\mkos\winremount /Add-Package /PackagePath:D:\mkos\hotfix\all
         dism /Image:D:\mkos\winremount /Add-Driver /Driver:D:\mkos\drivers /Recurse /ForceUnsigned
         dism /Unmount-Wim /MountDir:D:\mkos\winremount /Commit
         dism /Unmount-Wim /MountDir:D:\mkos\mount /Commit

   - 索引 2：

         dism /Mount-WIM /WimFile:D:\mkos\os\sources\install.wim /Index:2 /MountDir:D:\mkos\mount
         dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\all
         dism /Image:D:\mkos\mount /Add-Driver /Driver:D:\mkos\drivers /Recurse /ForceUnsigned
         dism /Unmount-Wim /MountDir:D:\mkos\mount /Commit

   - 索引 3：

         dism /Mount-WIM /WimFile:D:\mkos\os\sources\install.wim /Index:3 /MountDir:D:\mkos\mount
         dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\all
         dism /Image:D:\mkos\mount /Add-Driver /Driver:D:\mkos\drivers /Recurse /ForceUnsigned
         dism /Unmount-Wim /MountDir:D:\mkos\mount /Commit

   - 索引 4：

         dism /Mount-WIM /WimFile:D:\mkos\os\sources\install.wim /Index:4 /MountDir:D:\mkos\mount
         dism /Image:D:\mkos\mount /Add-Package /PackagePath:D:\mkos\hotfix\all
         dism /Image:D:\mkos\mount /Add-Driver /Driver:D:\mkos\drivers /Recurse /ForceUnsigned
         dism /Unmount-Wim /MountDir:D:\mkos\mount /Commit

    至此，完成对 install.wim 的操作。

5. 加入 UEFI 引导支持

    复制 C:\Windows\Boot\EFI\bootmgfw.efi 文件到 D:\mkos\os\efi\boot 文件夹下（新建一个），并改名为 bootx64.efi。

6. 给 install.wim 瘦身

    经过注入后的影响文件体积是比较大的，不方便我们的刻盘安装，要先对它进行压缩。

    以管理员身份打开“部署工具命令提示”，依次输入以下命令

         imagex /compress maximum /export D:\mkos\os\sources\install.wim 1 D:\mkos\install.wim
         imagex /compress maximum /export D:\mkos\os\sources\install.wim 2 D:\mkos\install.wim
         imagex /compress maximum /export D:\mkos\os\sources\install.wim 3 D:\mkos\install.wim
         imagex /compress maximum /export D:\mkos\os\sources\install.wim 4 D:\mkos\install.wim
         copy /y D:\mkos\install.wim D:\mkos\os\sources\install.wim

7. 打包成ISO镜像
继续在刚才的命令提示下，输入以下命令，注意空格：

         oscdimg -LNewWindows7 -m -u2 -bootdata:2#p0,e,bD:\mkos\os\boot\etfsboot.com#pEF,e,bD:\mkos\os\efi\microsoft\boot\efisys.bin D:\mkos\os D:\mkos\NewWin7.iso