# Bootstrap your Raspberry Pi

## Install Raspbian on a SD card

* Download the [latest Raspbian lite image][1] from the [download page][2].
* Download and install [Etcher][3].
* Open Etcher and flash the OS image to an SD card.

[1]: https://downloads.raspberrypi.org/raspbian_lite_latest
[2]: https://www.raspberrypi.org/downloads/raspbian/
[3]: https://etcher.io/

## Enable headless access
* Mount the SD card on your computer
* Put an empty file named `ssh` in the boot partition to enable ssh.
    sudo touch /Volumes/boot/ssh

## Enable Serial Console

* Mount the SD card on your computer
* Open file for edit named `config.txt` in the boot partition.
* Add `enable_uart=1` config.txt
* On Raspberry Pi 3 `dtoverlay=pi3-disable-bt`

## Initial setup

* Put the SD card into the Raspberry Pi and boot the device.
* Log in with the default credentials (pi/raspberry).
