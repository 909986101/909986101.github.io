# USB3.0 + NVMe SSD

> 使用 `DISM` 或制造商提供的工具，实现 Windows 7 安装镜像对 USB3.0 和 NVMe SSD 的支持

## 方法

1. 使用 `DISM` 注入驱动和补丁

2. 使用制造商工具将 USB3.0、NVMe SSD 驱动整合进安装介质

制造商工具是调用 `DISM` 来实现注入的，因为使用用户图形界面操作简单不易出错。

制造商工具软件包含了所需的驱动和补丁文件。

## 使用制造商工具

|制造商|工具名称|
|:--|:--|
|华硕|`ASUS EZ Installer`|
|技嘉|`WindowsImageTool`|

根据软件提示，逐步操作可轻松完成

## 使用 DISM

详见：[使用 DISM 为 Windows 7 注入 USB3.0 和 NVMe 驱动](win7-injection-usb3-nvme.md)

## 问题

### 300 系列主板

- 仅 H310C 和 B365 有适配 Windows 7 的 USB 3.0 驱动。
- 自 8 代酷睿起，Intel 不再提供适配 Windows 7 核显驱动，安装时需要独显。

### NVMe SSD

- 在 32 位系统上会出现“蓝屏”，建议 64 位系统。

### Legacy + MBR

- USB3.0 和 NVMe SSD 均支持。