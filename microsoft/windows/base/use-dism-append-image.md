# 使用 DISM 制作多合一系统镜像

本文以 Windows 7 VL 专业版 32 位、64 位集成同一 .WIM 文件中为例。本文适用于 Win7、8、8.1、10 及 Windows Server 2008 R2、2012、2016、2019 等

## 准备

### 获取 .WIM 文件

### 查看镜像文件信息

```
DISM /Get-ImageInfo /ImageFile:F:\sources\install.wim
```

## 执行

### 集成镜像

```
DISM /Export-Image /SourceImageFile:F:\sources\install.wim /SourceIndex:1 /DestinationImageFile:C:\win7pro_vl\install.wim /DestinationName:"Windows 7 Pro VL x86"

DISM /Export-Image /SourceImageFile:G:\sources\install.wim /SourceIndex:1 /DestinationImageFile:C:\win7pro_vl\install.wim /DestinationName:"Windows 7 Pro VL x64"
```

F 盘挂载 x86 镜像  
G 盘挂载 x64 镜像

集成 x64、x86 中索引1（VL 专业版）到文件 `C:\win7pro_vl\install.wim`

## 参考

> https://docs.microsoft.com/zh-cn/windows-hardware/manufacture/desktop/dism-image-management-command-line-options-s14