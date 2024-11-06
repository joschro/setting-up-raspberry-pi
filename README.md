Setting up a Raspberry Pi 
=========================
Install options for the Raspberry Pi (all versions)

Detailed hardware information for all versions: https://de.wikipedia.org/wiki/Raspberry_Pi
Overview of distributions available on Raspberry Pi: https://elinux.org/RPi_Distributions

Raspberry Pi compatibility
--------------------------
| OS            | Version   | Variant  | | Zero       | Zero W / WH | Zero 2 W   | 1 Mod. A   | 1 Mod. A+  | 1 Mod. B   | 1 Mod. B+  |	2 Mod. B  | 2 Mod. B v1.2 | 3 Mod. A+    | 3 Mod. B   | 3 Mod. B+  | 4 Mod. B   | 5          |
| ------------- | --------- | -------- |-| ---------- | ----------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ------------- | ------------ | ---------- | ---------- | ---------- | ---------- |
|               |           | CPU      | |ARMv6 32-bit|ARMv6 32-bit |ARMv8 64-bit|ARMv6 32-bit|ARMv6 32-bit|ARMv6 32-bit|ARMv6 32-bit|ARMv7 32-bit|ARMv8 64-bit   |ARMv8 64-bit  |ARMv8 64-bit|ARMv8 64-bit|ARMv8 64-bit|ARMv8 64-bit|
|               |           | RAM      | | 512 MB     | 512MB       | 512 MB     | 256 MB     | (512 MB)   | (512 MB)   | 512 MB     | 1 GB       | 1 GB          | 512 MB       | 1 GB       | 1 GB       | 1/2/4/8 GB | 4/8 GB     |
| CentOS        | 7         |          | |            |                                                            |                                                           |          |           |          |           |          |               |           |          |           |          |          |
| CentOS        | 8         |          | |            |                                                            |                                                           |          |           |          |           |          |               |           |          |           |          |          |
| CentOS        | 8 Stream  |          | |            |                                                            |                                                           |          |           |          |           |          |               |           |          |           |          |          |
| CentOS        | 9 Stream  |          | |            |                                                            |[(X)](#centos-9-stream-on-raspberry-pi-zero-2-w)           |          |           |          |           |          |               |           |          |           |          |          |
| Fedora        | 37        | XFCE Spin| |            |                                                            |[X](#fedora-37-xfce-on-raspberry-pi-zero-2-w)               |          |           |          |           |          |               |           |          |           |          |          |
| Fedora        | 39        | IoT      | |            |                                                            |[X](#fedora-39-iot-on-raspberry-pi-zero-2-w)               |          |           |          |           |          |               |           |          |           |          |          |
| Fedora        | 39        | Minimal  | |            |                                                            |[X](#fedora-39-minimal-on-raspberry-pi-zero-2-w)           |          |           |          |           |          |               |           |          |           |          |          |
| Fedora        | 39        | KDE Spin | |            |                                                            |                                                           |          |           |          |           |          |               |           |          |           |[X](#fedora-39-kde-on-raspberry-pi-4-b)|          |          |
| Fedora        | 40        | Minimal  | |            |                                                            |[X](#fedora-40-minimal-on-raspberry-pi-zero-2-w)           |          |           |          |           |          |               |           |          |           |          |          |
| Fedora        | 40        | KDE Spin | |            |                                                            |                                                           |          |           |          |           |          |               |           |          |           |[X](#fedora-40-kde-on-raspberry-pi-4-b)|          |          |
| RaspiOS       |           |          | |            |                                                            |[X](#raspios-on-raspberry-pi-zero-2-w)                     |          |           |          |           |          |               |           |          |           |          |          |
| RedSleeve     | 6         |          | |            |[X](#redsleeve-6-on-raspberry-pi-zero-raspberry-pi-zero-wwh)|                                                           |          |           |          |           |          |               |           |          |           |          |          |
| RedSleeve     | 7         |          | |            |[X](#redsleeve-7-on-raspberry-pi-zero-raspberry-pi-zero-wwh)|                                                           |          |           |          |           |          |               |           |          |           |          |          |
| RedSleeve     | 8         |          | |            |[X](#redsleeve-8-on-raspberry-pi-zero-raspberry-pi-zero-wwh)|[X](#redsleeve-8-on-raspberry-pi-zero-2-w)                 |          |           |          |           |          |               |           |          |           |          |          |

# CentOS
Upstream Red Hat Enterprise Linux: ```http://mirror.centos.org/altarch/``` or ```http://isoredirect.centos.org/altarch/```

## CentOS 7 on Raspberry Pi TBD
## CentOS 8 on Raspberry Pi TBD
## CentOS 8 Stream on Raspberry Pi TBD
## CentOS 9 Stream on Raspberry Pi Zero 2 W
* Download image: https://people.centos.org/pgreco/CentOS-Userland-9-stream-aarch64-RaspberryPI-Minimal-4/CentOS-Userland-9-stream-aarch64-RaspberryPI-Minimal-4-sda.raw.xz
* Write image to sd card
    ```
    arm-image-installer --resizefs --target=rpi02w --image=/home/<YOUR_USER>/Downloads/CentOS-Userland-9-stream-aarch64-RaspberryPI-Minimal-4-sda.raw.xz--media=/dev/sdX
    ```
* Login with
  ```
  localhost login: root
  Password: centos
  ```
  and set your local keyboard
  ```
  loadkeys de
  ```
* If you haven't used the ```--resizefs``` option above to use all available space on sd card, either add a 4th partition with parted or enlarge 3rd partition:
    ```
    # enlarge the 3rd partition (this example uses mmcblk0)
    growpart /dev/mmcblk0 3
    # grow the volume to take up the rest of the disk
    resize2fs /dev/mmcblk0p3
* Activate wifi
  ```
  [root@localhost ~ ]# nmtui
  ```
  then ```Activate a connection```.

> [!NOTE]
> Seems not to work, no SSID is showing up; connecting wired network works to update, but afterwards network is not coming up - brmcfmac module crashes.


# Fedora
https://fedoraproject.org/wiki/Architectures/ARM/Raspberry_Pi

## Fedora 37 XFCE on Raspberry Pi Zero 2 W
* Download image: https://download.fedoraproject.org/pub/archive/fedora-secondary/releases/37/Spins/aarch64/images/Fedora-Xfce-37-1.7.aarch64.raw.xz
* Write image to sd card
    ```
    arm-image-installer --showboot --resizefs --target=rpi02w --image=/home/<YOUR_USER>/Downloads/Fedora-Minimal-39-1.5.aarch64.raw.xz --media=/dev/sdX
    ```

* You'll probably want more available RAM, only solution is to add SWAP space:
    ```
    dd if=/dev/zero of=/swap.file bs=4M count=256
    mkswap /swap.file
    chmod 0600 /swap.file
    swapon /swap.file
    echo -e "/swap.file\tswap\tswap\tdefaults\t0\t0" >> /etc/fstab
    ```

## Fedora 39 IoT on Raspberry Pi Zero 2 W

* Download image: https://download.fedoraproject.org/pub/alt/iot/39/IoT/aarch64/images/Fedora-IoT-39.20231103.1-20231103.1.aarch64.raw.xz

    See https://docs.fedoraproject.org/en-US/iot/ for more info.
    
    https://www.redhat.com/sysadmin/fedora-iot-raspberry-pi
    https://www.redhat.com/sysadmin/ansible-automate-fedora-iot-config
    ```
    arm-image-installer --norootpass --resizefs --target=rpi02w --addkey=/home/<YOUR_USER>/.ssh/id_rsa.pub --image=/home/<YOUR_USER>/Downloads/Fedora-IoT-39.20231103.1-20231103.1.aarch64.raw.xz --media=/dev/sdX
    ```

* Activate wifi for IoT images
    ```
    # mount partition 3 and create wifi01.nmconnection in
    /mnt/ostree/deploy/fedora-iot/deploy/d06...0f.0/etc/NetworkManager/system-connections/
    # with the following content:
    [connection]
    id=wifi01
    type=wifi
    permissions=
    autoconnect=true
    
    [wifi]
    mac-address-blacklist=
    mode=infrastructure
    ssid=wifissid
    
    [wifi-security]
    auth-alg=open
    key-mgmt=wpa-psk
    psk=********************************************
    
    [ipv4]
    dns-search=
    method=auto
    
    [ipv6]
    addr-gen-mode=stable-privacy
    dns-search=
    method=auto
    
    [proxy]

    # finally, change file permission to
    chmod 600 wifi01.nmconnection
    ```
* Either look up the IP address of the Raspberry Pi in your router or login using root and no password, then issue
  ```
  ip add sh
  ```
* Login via ssh using your ssh public key like
  ```
  ssh -i /home/<YOUR_USER>/.ssh/id_rsa.pub root@<ip_of_your_raspberry>
  ```
* Add packages and update:
    ```
    rpm-ostree status
    rpm-ostree install cockpit cockpit-podman && firewall-cmd --add-service cockpit --permanent && rpm-ostree upgrade && systemctl reboot
    systemctl enable --now cockpit.socket
    useradd -G wheel -c "Tux Pinguin" -m -U tux
    passwd tux
    ```

## Fedora 39 Minimal on Raspberry Pi Zero 2 W
* Download image: https://download.fedoraproject.org/pub/fedora-secondary/releases/39/Spins/aarch64/images/Fedora-Minimal-39-1.5.aarch64.raw.xz
* Write image to sd card
    ```
    arm-image-installer --resizefs --target=rpi02w --image=/home/<YOUR_USER>/Downloads/Fedora-Minimal-39-1.5.aarch64.raw.xz --media=/dev/sdX
    ```
* If you haven't used the ```--resizefs``` option above to use all available space on sd card, either add a 4th partition with parted or enlarge 3rd partition:
    ```
    # enlarge the 3rd partition (this example uses mmcblk0)
    growpart /dev/mmcblk0 3
    # grow the volume to take up the rest of the disk
    resize2fs /dev/mmcblk0p3
    # resize root partition for the armhfp server image (which uses xfs)
    xfs_growfs -d /
    ```
* Activate wifi for minimal and server images:
    ```
    # list of networks
    nmcli device wifi list
    # connect
    nmcli device wifi connect $SSID --ask
    # in case of failure due to wrong password remove connection
    nmcli con delete $SSID
    # before connecting again
    ```

* You'll probably want more available RAM, only solution is to add SWAP space:
    ```
    dd if=/dev/zero of=/swap.file bs=4M count=256
    mkswap /swap.file
    chmod 0600 /swap.file
    swapon /swap.file
    echo -e "/swap.file\tswap\tswap\tdefaults\t0\t0" >> /etc/fstab
    ```

## Fedora 39 KDE on Raspberry Pi 4 B
* Download image: https://download.fedoraproject.org/pub/fedora-secondary/releases/39/Spins/aarch64/images/Fedora-KDE-39-1.5.aarch64.raw.xz
* Write image to sd card
    ```
    arm-image-installer --resizefs --target=rpi4 --image=/home/<YOUR_USER>/Downloads/Fedora-KDE-39-1.5.aarch64.raw.xz --media=/dev/sdX
    ```
* If you haven't used the ```--resizefs``` option above to use all available space on sd card, either add a 4th partition with parted or enlarge 3rd partition:
    ```
    # enlarge the 3rd partition (this example uses mmcblk0)
    growpart /dev/mmcblk0 3
    # grow the volume to take up the rest of the disk
    resize2fs /dev/mmcblk0p3
    # resize root partition for the armhfp server image (which uses xfs)
    xfs_growfs -d /
    ```

## Fedora 40 Minimal on Raspberry Pi Zero 2 W
* Download image: [https://download.fedoraproject.org/pub/fedora-secondary/releases/39/Spins/aarch64/images/Fedora-Minimal-39-1.5.aarch64.raw.xz](https://d2lzkl7pfhq30w.cloudfront.net/pub/fedora/linux/releases/40/Server/aarch64/images/Fedora-Server-40-1.14.aarch64.raw.xz)
* Write image to sd card
    ```
    arm-image-installer --resizefs --target=rpi02w --image=/home/<YOUR_USER>/Downloads/Fedora-Server-40-1.14.aarch64.raw.xz --media=/dev/sdX
    ```
* If you haven't used the ```--resizefs``` option above to use all available space on sd card, either add a 4th partition with parted or enlarge 3rd partition:
    ```
    # enlarge the 3rd partition (this example uses mmcblk0)
    growpart /dev/mmcblk0 3
    # grow the volume to take up the rest of the disk
    resize2fs /dev/mmcblk0p3
    # resize root partition for the armhfp server image (which uses xfs)
    xfs_growfs -d /
    ```
* Activate wifi for minimal and server images:
    ```
    # list of networks
    nmcli device wifi list
    # connect
    nmcli device wifi connect $SSID --ask
    # in case of failure due to wrong password remove connection
    nmcli con delete $SSID
    # before connecting again
    ```

* You'll probably want more available RAM, only solution is to add SWAP space:
    ```
    dd if=/dev/zero of=/swap.file bs=4M count=256
    mkswap /swap.file
    chmod 0600 /swap.file
    swapon /swap.file
    echo -e "/swap.file\tswap\tswap\tdefaults\t0\t0" >> /etc/fstab
    ```

## Fedora 40 KDE on Raspberry Pi 4 B
* Download image: https://download.fedoraproject.org/pub/fedora-secondary/releases/40/Spins/aarch64/images/Fedora-KDE-40-1.14.aarch64.raw.xz or newer
* Write image to sd card
    ```
    arm-image-installer --resizefs --target=rpi4 --image=/home/<YOUR_USER>/Downloads/Fedora-KDE-40-1.14.aarch64.raw.xz --media=/dev/sdX
    ```
* If you haven't used the ```--resizefs``` option above to use all available space on sd card, either add a 4th partition with parted or enlarge 3rd partition:
    ```
    # enlarge the 3rd partition (this example uses mmcblk0)
    growpart /dev/mmcblk0 3
    # grow the volume to take up the rest of the disk
    resize2fs /dev/mmcblk0p3
    # resize root partition for the armhfp server image (which uses xfs)
    xfs_growfs -d /
    ```
* before booting into the installer you need to edit the kernel option in the grub menu when installing Fedora-KDE-40-1.14.aarch64.raw.xz to workaround a graphics bug of the installer making it impossible to do the installation:
  * hit ```<e>``` when the grub boot menu shows up
  * move the cursor down 3 lines to the kernel command line and press ```<end>``` to move the cursor to the end of the line
  * enter
      ```
      nomodeset
      ```
  * enter ```<ctrl>```-```<x>``` to boot with the modified boot options
  * after successful installation, you'll be left with a cursor on a black screen; press ```<ctrl>```-```<alt>```-```<3>``` to get to the text console and hit ```<ctrl>```-```<alt>```-```<del>``` to reboot the system. No the system should boot into the graphical login screen

# RaspiOS
* Download image: https://www.raspberrypi.com/software/operating-systems/

## RaspiOS on Raspberry Pi Zero 2 W
* Download image: any of https://www.raspberrypi.com/software/operating-systems/ provided images
* Under Linux, write the image to an SD card, e.g.
  ```
  unzip -p 2022-01-28-raspios-bullseye-armhf-lite.zip | dd status=progress bs=4M of=/dev/sda && sync;sync;sync
  ```

* For graphical desktop images, just insert SD card and power up; follow the instructions displayed
* For text only command line images, just insert SD card and power up; login with username ```pi``` and password ```raspberry``` and enter:
  ```
  sudo raspi-config
  ```
  
* For headless operation (no monitor, no keyboard attached), you need to prepare the installed operating system to be accessible via Wifi:
  * For RaspiOS up to Bullseye
    * Mount the /boot partition (in this case to /run/media/joschro/bootfs); create a file called "ssh" in the boot partition, e.g.
      ```
      touch /run/media/joschro/bootfs/ssh
      ```
    * In the same location, create a file called wpa_supplicant.conf with
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
    
  * For RaspiOS from Bookworm or later
    * Mount the /boot partition (in this case to /run/media/joschro/bootfs);create a file called "custom.toml" in the boot partition with
      ```
      # Required:
      config_version = 1

      [system]
      hostname = "raspberrypi"

      [user]
      # If present, the default "pi" user gets renamed to this "name"
      name = "pi"
      # The password can be encrypted or plain. To encrypt, we can use "openssl passwd -5 raspberry"
      password = "$5$gi4yf1aU9lHD1DRD$IHsbDIrC2UtmW8Q.qD2cTcrbLJ1zc6iV1oCT7FeDLb1"
      password_encrypted = true
      
      [ssh]
      # ssh_import_id = "gh:user" # import public keys from github
      enabled = true
      password_authentication = false
      # We can also seed the ssh public keys configured for the default user:
      # authorized_keys = [ "ssh-rsa ... user@host", ... ]

      [wlan]
      ssid = "mywifi"
      password = "$5$pN7oRnie.WDOHoJY$aWEYmKUytN/S/bxMza5ksBiurbSJmcvcysBKHSmYa45"
      password_encrypted = true
      hidden = false
      # The country is written to /etc/default/crda
      # Reference: https://wireless.wiki.kernel.org/en/developers/Regulatory
      country = "DE"

      [locale]
      keymap = "de"
      timezone = "Europe/Berlin"
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

# RedSleeve
https://redsleeve.fandom.com/wiki/Install_on_a_Raspberry_Pi

## RedSleeve 6 on Raspberry Pi Zero, Raspberry Pi Zero W / WH
* Download image: https://www.mirrorservice.org/sites/ftp.redsleeve.org/pub/el6/rootfs/

## RedSleeve 7 on Raspberry Pi Zero, Raspberry Pi Zero W / WH
* Download image: https://www.mirrorservice.org/sites/ftp.redsleeve.org/pub/el7-devel/el7/rootfs/

* Download *raspi-redsleeve7.4-cli-1.0.img.xz* (or any newer release) from [Github](https://github.com/redsleeve-linux/redsleeve-linux.github.io/releases/tag/rpi-7.4-1.0)
* Write RedSleeve to an SD card with  
  ```xzcat /run/media/jschrode/Drive1/Images/raspi-redsleeve7.4-cli-1.0.img.xz | dd status=progress bs=4M of=/dev/sda```
* Login with ```rpi login: root``` and ```Password: password1234```
* Change keyboard layout to your locale with  
  ```[root@rpi ~]# loadkeys de```  
  for german layout
* Make keyboard layout permanent with  
 ```[root@rpi ~]# localectl set-keymap de```
* Change root password with  
  ```[root@rpi ~]# passwd```
* Set up networking with  
  ```[root@rpi ~]# nmtui```
  - select ```Activate a connection```
  - choose a Wifi from the list to connect to and provide the password when prompted
  - select ```<Back>```
  - select ```Set system hostname``` and provide a meaningful name for the system
  - select ```Quit``` and confirm with ```<OK>```
  - use the command ```ifconfig``` to show the IP address the RPi got from the DHCP server
* Resize root filesystem with  
  ```[root@rpi ~]# fdisk /dev/mmcblk0```
  - type ```d``` and accept with ```<Enter>```
  - type ```n``` and accept all questions with ```<Enter>```
  - type ```w``` and ```<Enter>``` to write and exit fdisk
  - enter  
    ```[root@rpi ~]# reboot``` to reboot the system and re-read partition table
  - login as root with the password you set above
  - enter  
    ```[root@rpi ~]# resize2fs /dev/mmcblk0p2``` to resize the root filesystem
* Install required software with 
  - ```[root@rpi ~]# yum -y install epel-release```
  - ```[root@rpi ~]# yum -y install git ansible vim screen```
  - ```[root@rpi ~]# yum -y update```
  and activate updated packages with
  - ```[root@rpi ~]# reboot```

## RedSleeve 8 on Raspberry Pi Zero, Raspberry Pi Zero W / WH
* Download image: https://www.mirrorservice.org/sites/ftp.redsleeve.org/pub/el8/8.0-first_run/rootfs/

* Install and boot one of https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-32-bit and then
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
        
## RedSleeve 8 on Raspberry Pi Zero 2 W
https://redsleeve.fandom.com/wiki/Install_on_a_Raspberry_Pi
A CentOS clone.

* Download an image from http://ftp.redsleeve.org/pub/ , e.g.
  ```
  http://ftp.redsleeve.org/pub/el8/8/rootfs/rsel8_root_img.tar.gz
  ```
  

Raspberry Pi 1 Mod. A, Raspberry Pi 1 Mod. A+, Raspberry Pi 1 Mod. B, Raspberry Pi 1 Mod. B+
---------------------

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

