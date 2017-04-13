So this is a modified bat file I made years ago. This payload is designed for Admins with no monitoring or who have just started a new job. 

This will make a folder on the root of C called Audits and then a sub folder and there will be two text files contained here. One txt file will have system info details and one will have a list of all installed programs. 

At the bottom of the script you can edit the Robocopy command to send the files anywhere you have permissions too (You may need to configure UAC entries) All the windows that were opened will close even if it is not in order.

feel free to tinker with this and make it your own. My handle is Phantom Santa because I drop random packets all round the world :P 

DELAY 2000
GUI r
DELAY 150
STRING CMD /ADMINISTRATOR 
DELAY 150
ENTER
DELAY 150
STRING CD c:\
DELAY 150
ENTER
STRING MD Audit
DELAY 150
ENTER
DELAY 150
STRING CD c:\Audit
DELAY 150
ENTER
DELAY 150
STRING MD Audit-%date:/=_%"
DELAY 70
ENTER
DELAY 1000
REM This variable is used so that robocopy can create a date stamped folder to help 
REM Id the folder 
STRING set DST=Audit-%date:/=_%
DELAY 1000
ENTER
DELAY 1000
STRING systeminfo.exe>C:\Audit\Audit-%date:/=_%"\systemSpecs.txt
ENTER
DELAY 250
STRING Exit
ENTER
GUI r 
DELAY 100
STRING POWERSHELL
DELAY 20
ENTER
DELAY 1000
STRING Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher, Size, InstallDate | Format-Table -AutoSize > C:\Audit\InstallList.txt
ENTER
DELAY 1000
STRING EXIT
DELAY 20 
ENTER
DELAY 320
GUI r
DELAY 100
STRING CMD
ENTER 
DELAY 150 
STRING ROBOCOPY "c:\Audit" "\\PC NETWORK PATH\Audits" /s /e /r:0 /w:0 /np
ENTER
DELAY 100
STRING ROBOCOPY "c:\Audit\Audit-%date:/=_%"" "\Audits" /s /e /r:0 /w:0 /np 
ENTER
DELAY 100
STRING EXIT
ENTER
REM Made by Phantom Santa  

