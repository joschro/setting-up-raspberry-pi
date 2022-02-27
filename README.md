setting-up-raspberry-pi
=======================
Install options for the Raspberry Pi (all versions)

Detailed information on all versions: https://de.wikipedia.org/wiki/Raspberry_Pi

Raspberry Pi Zero, Raspberry Pi Zero W / WH
-----------------------------------------
ARM6 32-bit

Raspberry Pi Zero 2 W
---------------------
### RaspiOS
* Download any of https://www.raspberrypi.com/software/operating-systems/ provided images.
* Under Linux, write the image to an SD card, e.g.
  ```unzip -p 2022-01-28-raspios-bullseye-armhf-lite.zip | dd status=progress bs=4M of=/dev/sda && sync;sync;sync```
* Mount both /boot and /root partitions; create a file called "ssh" in the boot partition, e.g.
  ```touch /run/media/joschro/boot/ssh```
  Edit etc/wpa_supplicant/wpa_supplicant.conf on the root partition of the mounted SD card, e.g.
  ```cat >> /run/media/jschrode/rootfs/etc/wpa_supplicant/wpa_supplicant.conf <<EOF
  country=DE
  
  network={
          ssid="myhomewifi"
          psk="myhomewifipassword"
  }```
  so it looks like this:
  ```
  ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
  update_config=1
  country=DE
  
  network={
          ssid="myhomewifi"
          psk="myhomewifipassword"
  }```
* Unmount both mount points, e.g.
  ```umount /run/media/joschro/*```

Raspberry Pi 1 Mod. A, Raspberry Pi 1 Mod. A+, Raspberry Pi 1 Mod. B, Raspberry Pi 1 Mod. B+
---------------------
ARM6, 32-bit

Raspberry Pi 2 Mod. B
---------------------

Raspberry Pi 2 Mod. B v1.2
---------------------

Raspberry Pi 3 Mod. A+
---------------------

Raspberry Pi 3 Mod. B
---------------------

Raspberry Pi 3 Mod. B+
---------------------

Raspberry Pi 4 Mod. B
---------------------
