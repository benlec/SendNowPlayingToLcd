# SendNowPlayingToLcd
Raspberry Pi scripts to send shairport metadata NowPlaying info to LCD screen

This is a set of scripts which get metadata info from ShairPort, read it and send it to an LCD screen plugged to your Raspberry Pi. I've made this for the Pimoroni dot3k (DisplayOTron 3000) screen but it can be adapted to any LCD I suppose. Here are the main steps explained bellow.

1°) Get and install all the pre-requisites:

1.1°) You need ShairPort to make your RPi able to get Airplay streams. Get this from here : https://github.com/abrasive/shairport
there is a good tutorial here http://raspberrypihq.com/how-to-turn-your-raspberry-pi-into-a-airplay-receiver-to-stream-music-fro
m-your-iphone/ make sure you read all the comments below the post. Some steps can fail so read the comments to get appropriate help

1.2°) You also need to setup your LCD Screen depending on the model you use. In my case i used Pimoroni dot3k. Get it here: https://github.com/pimoroni/dot3k

2°) Modify the Shairport Daemon in order to make it able to output NowPlaying metadata

This repository provides a Shairport Daemon file modified in order to
- Enable Metadata output to a given directory
- Cleanup NowPlaying file on startup
- Delete all the Cover files on startup

These cleanup are important to handle in order not to leave useless cached metadata info on the RPi box and start each session with a clean now_playing file. ShairPort simply append the NowPlaying into a file and never clean it up which complexify the reading of this file. It also never cleanup the Artwork Covers, it lets all the history sit there.

3°) Read Now_Playing Metadata information provided by Shairport and send it to LCD.

This repository provides a script to do so.

4°) Run a script in the background to monitory NowPlaying info changes in order to send them to LCD screen.

This repository provides a script to do so. Execution will be integrated to ShairPort daemon.
The scrirpt is based on one of the PyInotify Tutorial, you need to install PyInotify as well as a pre-requisite
http://github.com/seb-m/pyinotify
