# vlmcsd 超简单教程

**vlmcsd‌** 是一款开源的 KMS 模拟器，用于在本地或局域网内搭建密钥管理服务，模拟微软官方 KMS 服务器行为，实现 Windows 和 Office 的批量激活。

## Start Vlmcsd

github 地址：https://github.com/Wind4/vlmcsd

示例

```bash
# wget https://github.com/Wind4/vlmcsd/releases/download/svn1113/binaries.tar.gz
# tar xf binaries.tar.gz
# ./binaries/Linux/intel/static/vlmcsd-x64-musl-static
```

查看 1688 端口已打开

```
[root@localhost ~]# ss -ntl | grep 1688
LISTEN     0      128          *:1688                     *:*                  
LISTEN     0      128         :::1688                    :::*
```

开机启动

```bash
# cp ./binaries/Linux/intel/static/vlmcsd-x64-musl-static /usr/local/bin/
# echo '/usr/local/bin/vlmcsd-x64-musl-static' >> /etc/rc.d/rc.local
# chmod a+x /etc/rc.d/rc.local
```

## 测试

查看可用 apps

```shell
# ./binaries/Linux/intel/static/vlmcs-x64-musl-static -x
```

查看 kms 服务器 194 号 app，194 是 Office Professional Plus 2019

```shell
# ./binaries/Linux/intel/static/vlmcs-x64-musl-static -v -l 194 127.0.0.1
```

上面示例以 Linux 为例子，其他系统及平台类似

## 目录结构

`vlmcsd-xxx`：服务器

`vlmcs-xxx`：客户端

## 激活

kms 服务器只能激活 vl 版软件

示例：Windows 10 专业版

```powershell
slmgr /upk
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
slmgr /skms <kms's IP>
slmgr /ato
```

示例：Office 2016 vl on Windows 10

```powershell
cd 'C:\Program Files\Microsoft Office\Office16\'
cscript ospp.vbs /sethst:<kms's IP>
cscript ospp.vbs /act
cscript ospp.vbs /dstatus
```


## 序列号

```
Windows 10

[教育版]
YNMGQ-8RYV3-4PGQ3-C8XTP-7CFBY

[专业版]
W269N-WFGWX-YVC9B-4J6C9-T83GX

[企业版]
NPPR9-FWDCX-D2C8J-H872K-2YT43
```

