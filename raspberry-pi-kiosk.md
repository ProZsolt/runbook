
https://www.danpurdy.co.uk/web-development/raspberry-pi-kiosk-screen-tutorial/

### Install Raspbian to a SD card

https://www.raspberrypi.org/documentation/installation/installing-images/mac.md

```
diskutil list
```

```
diskutil unmountDisk /dev/diskN
sudo dd bs=1m if=image.img of=/dev/rdiskN
sudo diskutil eject /dev/rdiskN
```

### Set up wifi

https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md

```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

```
network={
    ssid="testing"
    psk="testingPassword"
}
```

### Booting to desktop

https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=133691
```
sudo apt-get install xserver-xorg
```

```
sudo apt-get install xinit
```

```
sudo apt-get install lxde-core lxterminal lxappearance
sudo apt-get install lightdm
```

### Install Chromium

https://www.raspberrypi.org/forums/viewtopic.php?t=121195

Chromium 48

packages can be find http://ports.ubuntu.com/pool/universe/c/chromium-browser/

```
wget http://ports.ubuntu.com/pool/universe/c/chromium-browser/chromium-browser-l10n_48.0.2564.82-0ubuntu0.15.04.1.1193_all.deb
wget http://ports.ubuntu.com/pool/universe/c/chromium-browser/chromium-browser_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
wget http://ports.ubuntu.com/pool/universe/c/chromium-browser/chromium-codecs-ffmpeg-extra_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
```

```
sudo dpkg -i chromium-codecs-ffmpeg-extra_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
sudo dpkg -i chromium-browser-l10n_48.0.2564.82-0ubuntu0.15.04.1.1193_all.deb chromium-browser_48.0.2564.82-0ubuntu0.15.04.1.1193_armhf.deb
```

For dependenies
```
sudo apt-get -f install
```
### Start Chromium

```
sudo apt-get install x11-xserver-utils
```

```
vi ~/.config/lxsession/LXDE/autostart
```

```
@lxpanel --profile LXDE
@pcmanfm --desktop --profile LXDE

@xset s off
@xset -dpms
@xset s noblank

@chromium-browser --noerrdialogs --disable-infobars --disable-session-crashed-bubble --kiosk http://cheppers-gifmachine.herokuapp.com
```

### Remove mouse

```
sudo apt-get install unclutter
```

### Automaticali start and stop

I use crontab and two simple scripts to turn off the monitors after work and during the weekends.

In /home/pi create two files: screen_off.sh and screen_on.sh

screen_off.sh:
```
#!/bin/sh
tvservice --off
```

screen_on.sh:
```
#!/bin/sh
tvservice -p
fbset -depth 8; fbset -depth 16; xrefresh
```

Then, in the console type:
```
crontab -e
```

in the file, add the following 2 lines (line 1 turns on the screen every morning at 8am Mon-Fri; line 2 shuts it off every evening at 8pm Mon-Fri)
```
00 08 * * 1-5 /bin/bash /home/pi/screen_on.sh
00 20 * * 1-5 /bin/bash /home/pi/screen_off.sh
```

### Hide the boot text and logo

/boot/cmdline.txt:  
change `console=tty1` to `console=tty3`  
add `logo.nologo loglevel=3`.

### Witout window managment
https://github.com/MobilityLab/TransitScreen/wiki/Raspberry-Pi

```
xinit /usr/bin/chromium-browser --noerrdialogs --disable-infobars --disable-session-crashed-bubble --kiosk
```

~/.config/chromium/Default/Preferences
```
"window_placement": {                                                      
    "bottom": 1080,
    "left": 0,
    "maximized": true,
    "right": 1920,
    "top": 0,
    "work_area_bottom": 1080,
    "work_area_left": 0,
    "work_area_right": 1920,
    "work_area_top": 0
 }
```

### Backup
```
sudo dd if=/dev/disk3 of=gifmachine.img
```
