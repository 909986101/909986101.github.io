[Windows 7激活文件备份及恢复方法]

## 备份

备份激活文件.bat
```bat
@echo off
copy %windir%\System32\spp\tokens\pkeyconfig\pkeyconfig.xrm-ms
copy %windir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform\tokens.dat
pause
exit
```

## 激活

```bat
@echo off
net stop sppsvc /y
takeown /f "%WinDir%\System32\spp\tokens\pkeyconfig\pkeyconfig.xrm-ms"
cacls "%WinDir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform\tokens.dat" /e /g everyone:f
cacls "%WinDir%\System32\spp\tokens\pkeyconfig\pkeyconfig.xrm-ms" /e /g everyone:f
ren "%WinDir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform\tokens.dat" "tokens.bak"
ren "%WinDir%\System32\spp\tokens\pkeyconfig\pkeyconfig.xrm-ms" "pkeyconfig.bak"
copy tokens.dat "%WinDir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform\"
copy pkeyconfig.xrm-ms "%WinDir%\System32\spp\tokens\pkeyconfig\"
del "%WinDir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform\tokens.bak"
del "%WinDir%\System32\spp\tokens\pkeyconfig\pkeyconfig.bak"
net start sppsvc
cscript %windir%\system32\slmgr.vbs -ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX
cscript %windir%\system32\slmgr.vbs -ato
pause
exit
```

## 注意

其中的 “XXXXX-XXXXX-XXXXX-XXXXX-XXXXX” 是激活系统时使用的密钥