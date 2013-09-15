1. REM Author: Cody Theodore
1. REM Title: OSX Youtube Blast
1. REM This payload will open terminal, crank up the Macs volume all the way, then open a youtube video of your choice by replacing the link. Remember to include the "watch_popup" part of the URL for full screen.
1. DELAY 1000
1. GUI SPACE
1. STRING terminal
1. DELAY 500
1. ENTER
1. DELAY 4000
1. STRING osascript -e 'set volume 7'
1. DELAY 500
1. ENTER
1. DELAY 500
1. STRING open http://www.youtube.com/watch_popup?v=dQw4w9WgXcQ
1. DELAY 500
1. ENTER