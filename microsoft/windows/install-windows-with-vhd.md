# Windows 安装 VHD 方式

## 准备vhd文件

```
C:\WINDOWS\system32>diskpart
DISKPART> CREATE VDISK FILE=D:\win7.vhdx MAXIMUM=51200 TYPE=EXPANDABLE
DISKPART> ATTACH VDISK
```

## 提取 install.wim

位于安装光盘中 source 文件夹下

## 查看 install.wim 信息

```
dism /get-imageinfo /imagefile:install.wim
```

## 应用镜像

```
dism /apply-image /imagefile:install.wim /index:3 /applydir:Z:\
```

## 添加 boot

```
bcdboot Z:\windows /l zh-cn
```