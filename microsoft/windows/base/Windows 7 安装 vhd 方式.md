1. 准备vhd文件

        C:\WINDOWS\system32>diskpart
        DISKPART> CREATE VDISK FILE=D:\win7.vhdx MAXIMUM=51200 TYPE=EXPANDABLE
        DISKPART> ATTACH VDISK

1. 提取install.wim
   - 安装光盘中source文件夹下

1. 查看install.wim信息

        X:\image>Dism.exe /get-imageinfo /imagefile:install.wim

1. 应用镜像

        X:\image>dism.exe /apply-image /imagefile:install.wim /index:3 /applydir:Z:\

1. 添加boot

        bcdboot Z:\windows /l zh-cn