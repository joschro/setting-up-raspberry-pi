setting-up-raspberry-pi
=======================
Install options for the Raspberry Pi (all versions)

Detailed information on all versions: https://de.wikipedia.org/wiki/Raspberry_Pi

Raspberry Pi Zero, Raspberry Pi Zero W / WH
-----------------------------------------
ARM6 32-bit

### RedSleeve
https://redsleeve.fandom.com/wiki/Install_on_a_Raspberry_Pi

* RHEL 6: https://www.mirrorservice.org/sites/ftp.redsleeve.org/pub/el6/rootfs/
* RHEL 7: https://www.mirrorservice.org/sites/ftp.redsleeve.org/pub/el7-devel/el7/rootfs/
* RHEL 8: https://www.mirrorservice.org/sites/ftp.redsleeve.org/pub/el8/8.0-first_run/rootfs/

Install and boot one of https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-32-bit and then
    ```
    Mount the second partition of the card on your workstation. The rest of the instructions assume that this is partition2 and you have this mounted under /mnt.
    cd /mnt
    Backup the modules and firmware: tar -cf ~/raspi.tar etc/fstab lib/modules lib/firmware
    cd ~
    umount /mnt
    mke2fs -t ext4 partition2
    mount partition2 /mnt
    cd /mnt
    Extract the RedSleeve rootfs: tar --strip-components 1 -xjf ~/rsel6-rootfs.tar.bz2
    Restore the backed up files: tar -xf ~/raspi.tar
    cd etc
    vi fstab. Change root to mount from /dev/mmcblk0p2, /boot to mount from /dev/mmcblk0p1
    cd ~
    umount /mnt
    ```

Raspberry Pi Zero 2 W
---------------------
ARM8 64-bit

### RaspiOS
* Download any of https://www.raspberrypi.com/software/operating-systems/ provided images.
* Under Linux, write the image to an SD card, e.g.
  ```
  unzip -p 2022-01-28-raspios-bullseye-armhf-lite.zip | dd status=progress bs=4M of=/dev/sda && sync;sync;sync
  ```

* For graphical desktop images, just insert SD card and power up; follow the instructions displayed
* For text only command line images, just insert SD card and power up; login with username ```pi``` and password ```raspberry``` and enter:
  ```
  sudo raspi-config
  ```
  
* For headless operation (no monitor, no keyboard attached), you need to prepare the installes operating system to be accessible via Wifi:
  * Mount the /boot partition (in this case to /run/media/joschro/bootfs); create a file called "ssh" in the boot partition, e.g.
    ```
    touch /run/media/joschro/bootfs/ssh
    ```
  
  *  In the same location, create a file called wpa_supplicant.conf with e.g.  
```
cat > /run/media/joschro/bootfs/wpa_supplicant.conf <<EOF
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=DE

network={
        ssid="myhomewifi"
        psk="myhomewifipassword"
}
EOF
```
*    
  * Unmount the mount point, e.g.  
    ```
    umount /run/media/joschro/bootfs
    ```
  * Insert SD card and power up; look up any newly connected device in your router and determine the assigned IP address of your Raspberry Pi to connect via SSH with username ```pi``` and password ```raspberry```, e.g.:
    ```
    ssh pi@192.168.178.42
    ```
### Fedora
https://fedoraproject.org/wiki/Architectures/ARM/Raspberry_Pi

* Download TBD

### CentOS
Upstream Red Hat Enterprise Linux.

* Download any image from ```http://mirror.centos.org/altarch/``` or ```http://isoredirect.centos.org/altarch/```

### RedSleeve
https://redsleeve.fandom.com/wiki/Install_on_a_Raspberry_Pi
A CentOS clone.

* Download an image from http://ftp.redsleeve.org/pub/ , e.g.
  ```
  http://ftp.redsleeve.org/pub/el8/8/rootfs/rsel8_root_img.tar.gz
  ```
  

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
