#Video Looper for Raspbian Automatically play and loop fullscreen videos on a Raspberry Pi 2 or 3.

This system uses a basic bash script to play videos with omxplayer, it simply checks if omxplayer isn't running and then starts it again. This simple method seems to work flawlessly for weeks on end without freezing or glitches. The only caveat of this method is that there are approximately 2-3 seconds of black between each video. If you are looking to do something with gapless looping on Raspberry Pi, try Slooper by Matthias Dörfelt, though currently it needs a few updates to work without a remote (as of May 15, 2016).

There is a videolooper written in python that uses omxplayer by Adafruit, but unfortunately on testing looping videos for more than a day it froze (as of May 15, 2016).

The script will look for videos either in:

the video directory in the home directory of the pi user
a usb stick plugged in before startup (this will not be remounted if you pull it out and plug it back in)
#Installation

##Grab 'n Go Copy the prebuilt img to a micro SD card using these instructions. The img was setup using the steps below and 2016-05-10-raspbian-jessie-lite was used as the base raspbian image.

##Roll Your Own Start with a raspbian img, install it on the pi, and follow the steps below to install the videolooper.

###Install omxplayer

sudo apt-get update
sudo apt-get -y install omxplayer
###Setup auto mounting of usb stick

sudo mkdir -p /mnt/usbdisk
sudo echo \"/dev/sda1		/mnt/usbdisk	vfat	ro,nofail	0	0\" | sudo tee -a /etc/fstab
###Create folder for videos in home directory mkdir /home/pi/video

###Download startvideo.sh and put it in /home/pi/

cd /home/pi
wget https://raw.githubusercontent.com/timatron/videolooper-raspbian/master/startvideo.sh
chmod uga+rwx startvideo.sh
###Add startvideo.sh to .bashrc so it auto starts on login echo "/home/pi/startvideo.sh" | tee -a /home/pi/.bashrc

###Make system autoboot into pi user sudo raspi-config

Select option: "3 Boot Options"
Select option: "B2 Console Autologin"
###Expand your root partition if you want to sudo raspi-config

Select option: "1 Expand Filesystem"
