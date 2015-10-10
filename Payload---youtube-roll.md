A simple little payload by Aprizm which Youtube rolls a computer. 
```
REM Title: Youtube Roller
REM Author: Aprizm
REM Description: This scripts opens a youtube video in fullscreen and puts the browser in fullscreen
REM Option : if you change the link of the video dont forget to change the watch with watch_popup to have it fullscreen also add &loop=1 at the end to make it loop forever
DELAY 5000
GUI r
DELAY 50
STRING www.youtube.com/embed/qTkFw4q8CZw?rel=0&autoplay=1
ENTER
DELAY 1000
F11
