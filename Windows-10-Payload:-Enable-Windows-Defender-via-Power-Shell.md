If you wish to turn on real time protection (likely after turning it off earlier in your script) to remove the 'Turn on virus protection notification' that would otherwise be left behind, then the following step can be applied.

Windows defender can be enabled with PS using the following command

```ps
Set-MpPreference -DisableRealtimeMonitoring $false
```

An example script: 
Note: line with "ALT y" may not be required and could lead to error in the next line.  
```
REM Windows 10: Disable Windows Defender with Powershell
REM Author: Judge2020 with mod by Cfomodz
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
STRING Set-MpPreference -DisableRealtimeMonitoring $false
ENTER
STRING exit
ENTER
```