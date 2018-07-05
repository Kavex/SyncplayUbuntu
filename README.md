Syncplay: http://syncplay.pl/

VLC: http://www.videolan.org/


-------

###First we are going to add a user called syncplay with the option -r which flags the account as a system account. Next we need to make a dir for the syncplay files and give syncplay ownership to that folder.

```
sudo useradd -r syncplay
sudo mkdir /opt/syncplay
sudo chown syncplay /opt/syncplay
```

###Next we want to download the syncplay files and unpack them. The version of syncplay when this was wrote was 1.4.0 but make sure to check the website for latest updates.
```
cd /opt/syncplay
wget https://github.com/Syncplay/syncplay/archive/v1.5.4.tar.gz
tar -xvzf v1.5.4.tar.gz
cd /opt/syncplay/syncplay-1.5.4
```

###Syncplay requires python 2.7.* and a few dependencies
```
sudo apt-get install python python-pip
pip install twisted
pip install PySide
```

###Now we should be able to run the server but before you do, you'll need to learn a few options you use with launching.*
--------
`--port [port]` – Use stated port instead of the default one.

`--isolate-room` – If specified then ‘room isolation’ is enabled. This means that viewers will not be able to see information about users who are in rooms other than the one they are in. This feature is recommended for a public server, but not for a small private server.

`--password [password]` – Restrict access to the Syncplay server to only those who use this password when they connect to the server. This feature is recommended for a private server but is not needed for a public server. By default the password is blank (i.e. there is no password restriction). DO NOT USE A PASSWORD THAT YOU USE ANYWHERE ELSE!

`--salt [salt]`  – Random salt string used to generate controlled room passwords – needs to be the same for controlled room passwords to work between server instances

`--motd-file` [filepath] – Path to file from which motd will be fetched--motd-file [filepath] Path to file from which motd will be fetched

`--disable-ready` – Disables the readiness indicator feature

--------

###This is a quick command to get the server running with bare minimum options. We using a blank password and the default port of 8999. Of course you are expected to change the settings to fit you needs. Note: Change the --salt to something of your own atleast.
```
./syncplayServer.py --password  --port 8999 --salt saltpassword

```

###The server will close when we close the terminal window and we don't want that so we are going to use a program called Screen
```
sudo apt-get install screen
```

###Now we can run syncplay in a screen window so it doesn't close when we close the terminal
```
screen -S syncplay -d -m ./syncplayServer.py --password  --port 8999 --salt saltpassword
```

###Now we should be up and running and all you have to do is open the syncplay client on your desktop and connect to ip:8999

###You can find the latest version here

https://syncplay.pl/download/
