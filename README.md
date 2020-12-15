# raspi-image

[![ubuntu-20.04](https://img.shields.io/badge/ubuntu-20.04-brightgreen)](https://ubuntu.com/)
&nbsp;
[![ros-2](https://img.shields.io/badge/ros-2-brightgreen)](https://index.ros.org/doc/ros2/)
&nbsp;
[![raspi-4b](https://img.shields.io/badge/raspi-4B-brightgreen)](https://www.raspberrypi.org/)

This image is based on [Ubuntu Server 20.04.1 LTS 64-bit for Raspberry Pi 4](https://ubuntu.com/download/raspberry-pi).

## How to setup this image

### Setup Ubuntu on Raspberry Pi

Follow the instructions on [this site](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi) to install ubuntu on Raspberry Pi.

### Setup ROS 2

Follow the instructions on [this site](https://index.ros.org/doc/ros2/Installation/Foxy/Linux-Install-Debians/) to install ROS 2.

### Setup [gpiozero](https://gpiozero.readthedocs.io/en/stable/installing.html)

1. `sudo apt install python3-gpiozero`
2. `sudo addgroup gpio`
3. `sudo adduser ubuntu gpio`
4. `sudo adduser ubuntu i2c`
5. `sudo chown root:gpio /dev/gpiomem`
6. `sudo chmod g+rw /dev/gpiomem`
7. `exit` then re-login.
8. `groups ubuntu` to check if user `ubuntu` belongs to group `i2c` and `gpio`.
9. `sudo apt install python3-smbus`

### Setup [xow](https://github.com/medusalix/xow)

1. `sudo apt install cabextract`
2. `sudo apt install libusb-dev`
3. Follow the instructions on [this site](https://github.com/medusalix/xow#installation).

## Setup camera

1. Plug in camera (CSI port).
2. Download latest [raspi-config](http://archive.raspberrypi.org/debian/pool/main/r/raspi-config/), e.g. `wget http://archive.raspberrypi.org/debian/pool/main/r/raspi-config/raspi-config_20200817_all.deb`
3. `sudo dpkg -i raspi-config_20200817_all.deb`
4. `sudo apt --fix-broken install`
5. `sudo mount /dev/mmcblk0p1 /boot` (Run `df -h` to check the device number)
6. `sudo raspi-config`
7. Interfacing Options - Camera - Yes - Back - Finish - Reboot
8. `ls -al /dev/ | grep video` to check device `video0`
9. `sudo adduser ubuntu video`

## How to create this image

1. Insert SD card into Ubuntu Desktop.
2. Open `Disks`.
3. Select SD card.
4. Select `Create Disk Image` from menu.
5. `xz -k -v rpi.img`
