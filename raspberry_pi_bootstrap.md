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
```bash
sudo touch /Volumes/boot/ssh
```

## Edit config.txt
* Mount the SD card on your computer
* Open file for edit named `config.txt` in the boot partition.
```bash
vim /Volumes/boot/config.txt
```

### Enable serial console (optional)
* Add or edit the following line `enable_uart=1`
* On Raspberry Pi 3 also add `dtoverlay=pi3-disable-bt`

### Adjust gpu memory (optional)
* Add or edit the following line `gpu_mem=16`
* The minimum value is 16.
* The maximum value is 192, 448, or 944, depending on whether you are using a 256MB, 512MB, or 1024+MB Pi.

## Initial setup

* Put the SD card into the Raspberry Pi and boot the device.
* Log in with the default credentials (pi/raspberry).
