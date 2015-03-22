REM Author: Cameron Glass
<br>
REM Description: This payload opens a photo booth window and automatically takes a picture. Once this picture is taken, this payload proceeds to open terminal and tell it to say "You look ugly!". This payload is great for friends and family.
<br>
REM Credits: I must give all of the credit to Hak5 for their amazing product. This is my first payload and I hope it is a good one!
<br>
REM --------------------------------
<br>
DELAY 1000
<br>
GUI SPACE
<br>
DELAY 100
<br>
STRING photo booth
<br>
DELAY 100
<br>
ENTER
<br>
DELAY 1000
<br>
ENTER
<br>
DELAY 3000
<br>
GUI SPACE
<br>
STRING terminal
<br>
DELAY 100
<br>
ENTER
<br>
DELAY 1000
<br>
STRING say You look ugly!
<br>
DELAY 100
<br>
ENTER