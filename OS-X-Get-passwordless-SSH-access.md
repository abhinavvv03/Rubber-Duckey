
Author: Jesse Wallace (c0deous)

This script adds an ssh public key to the authorized_keys file on a target's mac. After running you can connect to the target computer with "ssh targetuser@targetcomputer" and you will be granted access without a password.  This a good alternative to the [OS X User Backdoor payload](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payload---OSX-User-Backdoor).  There are methods you can use: the web server method, and the twin duck method. The web server method requires you to have a web server (that the target can connect to), and you also must put your id_rsa.pub on your webserver. The twin duck method requires you to have the [Twin Duck firmware](http://code.google.com/p/ducky-decode/downloads/detail?name=c_duck_v2.1.hex&can=2&q=) [flashed](http://code.google.com/p/ducky-decode/wiki/Flashing_Guide) onto your ducky, and your id_rsa.pub needs to be at the root of the sd card. Also you need to name your ducky's sd card DUCKY. For more information on generating an id_rsa.pub read [this](https://www.digitalocean.com/community/articles/how-to-set-up-ssh-keys--2) (steps 1 & 2).  Note: I reccomend you use [duckencoder 2.6.3](http://code.google.com/p/ducky-decode/downloads/detail?name=DuckEncoder_2.6.3.zip&can=2&q=) to encode these. 

## Webserver Method
 
Replace SERVER with the address of your 
