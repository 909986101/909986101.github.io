# Windows 7 OEM 激活

> 使用 `cscript slmgr.vbs` 实现

## 前提

主板 bios 中包含 oem 信息

## 命令

```cmd
REM 导入证书
cscript %systemroot%\system32\slmgr.vbs -ilc %oemfile%.xrm-ms

REM 安装密钥
cscript %systemroot%\system32\slmgr.vbs -ipk %cdkey%
```