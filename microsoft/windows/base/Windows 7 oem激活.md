使用 `cscript slmgr.vbs` 实现

导入证书
```cmd
cscript %systemroot%\system32\slmgr.vbs -ilc %oemfile%.xrm-ms
```

安装密钥
```cmd
cscript %systemroot%\system32\slmgr.vbs -ipk %cdkey%
```