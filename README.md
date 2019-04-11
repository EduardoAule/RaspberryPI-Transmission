# RaspberryPI-Transmission

## Introduction
How  create a Download Server of Torrents with Raspberry PI and Transmission.

## Install
Open a terminal and type:

    sudo apt-get install transmission-daemon

## Create 2 directories
in my case I have created two directories:
    
    /home/pi/Downloads/myTorrents
and
    
    /home/pi/Downloads/mytmp

It is necessary to change the permissions to the directories to 770
    
    sudo chmod 770 /home/pi/Downloads/myTorrents
    sudo chmod 770 /home/pi/Downloads/mytmp

Transmission runs by default as user "debian-transmission". It is highly recommended not to change this due to security reasons.
However, we need Transmission to have the right to write to to these directories. 
We simply need, therefore, to add the "debian-transmission" user to the  "pi" group.
This is accomplished by entering the following command:

    sudo usermod -a -G pi debian-transmission

## Config Transmission
First step, stop the service:

    sudo /etc/init.d/transmission-daemon stop

Open with your favorite text editor this file:

    sudo nano /etc/transmission-daemon/settings.json

and change this values:

    "cache-size-mb”: 10,
    "download-dir”: "/path/to/downloads/complete",
    "incomplete-dir”: "/path/to/downloads/incomplete",
    "incomplete-dir-enabled”: true,
    "peer-port”: 51413,
    "preallocation”: 2,
    "rpc-enabled”: true,
    "rpc-password”: "your_pass",
    "rpc-port”: 9091,
    "rpc-username”: your_user,
    "rpc-whitelist”: "127.0.0.1”,
    "rpc-whitelist-enabled”: false,
    "umask”: 2

Note:
rpc-whitelist allows IP addresses to access the Web interface it has been set to all here. You can also change it to your local 
home network like 192.168.*.* if you want it to be more secure. However, if you want to be able to access transmission outside 
your local network then it should be *.*.*.* which represents all IPs.

    "rpc-whitelist": "*.*.*.*",

May as well disable the whitelist if you are allowing all IPs:

    "rpc-whitelist-enabled": false

## Start Transmission

    sudo /etc/init.d/transmission-daemon start
    
## Check Transmission in the Browser
Open your favorite browser and type:
    
    ip-raspberrypi:9091

Enter your username and pass.

![test](https://github.com/EduardoAule/RaspberryPI-Transmission/blob/master/transmission.png)
    
##Contributing

Please let me know if you would like to contribute any Actions or other features! Also please inquire me about any issues or confusion in documentation.
