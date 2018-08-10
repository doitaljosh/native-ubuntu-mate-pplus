# native-ubuntu-mate-pplus

Native Ubuntu MATE 18.04 for the LG V10:

This project is aimed towards developing a fully working Ubuntu desktop system on the under-estimated, under-rated, LG V10 Smartphone.
There is a very poor development community behind this particular model of smartphone, so chances are, those who have upgraded likely
have thrown this thing in a desk drawer and forgotten about it. But take it out of that desk drawer, because this is a fully booting
native Ubuntu rootfs and kernel which boots on the T-Mobile LG V10, and should boot on other variants with a kernel/config swap.

This is everything that works as of now:

- Graphics (fbdev, llvmpipe, and msm-fb-refresher)
- Touch (works natively with Xorg)
- 4G LTE data should work (might need modem firmware swap with different variants)
- Microphones (msm8994-tomtom-snd-card alsa UCM files from LG G4)
- Volume/power keys
- Pretty much stable systemd support
- Adsp, modem, and venus firmware blob bringup (with systemd script)
- USB ethernet and Ralink USB wireless support

And here's what I would love to also get working:

- Adreno 418 OpenGL Xorg 3D Acceleration (freedreno)
- Screen rotation
- Second screen omission
- Patch kernel for proper framebuffer refresh
- Backlight brightness control (udev rules)
- Audio output (maybe even the 32 bit HiFi DAC ;-), shouldn't be too hard to enable with alsactl save profiles)
- Sensors (Light sensor, proximity, laser rangefinder, etc, this phone has lots of them)
- ADB USB Debugging (probably not too hard at all)
- Cameras (libhybris android blob bringup)
- Hardware video decode
- And why not, of course, MAINLINE!

The rootfs was too big for GitHub so I uploaded it to Google Drive.

***Rootfs archive link***
[Download](https://drive.google.com/open?id=1AjhBs_9HLO0KC3bFpka2ewpuJTmigimK)

***Requirements:***

- A rooted LG V10 H901 with TWRP
- At least a 16GB SD Card if you want to boot from the SD card and keep Android
- A cup of coffee

***Instructions:***

- Copy the rootfs archive and desired boot image to whichever storage you're not using for Ubuntu
- Reboot your LG V10 into TWRP
- Backup your system, data, boot, if you feel you need to

***For installing to data partition:***
- Copy files to SD card
- Open Advanced>Terminal
- Type in these commands:
```shell
umount /dev/block/mmcblk0p53
```
```shell
make_ext4fs /dev/block/mmcblk0p53
```
```shell
mkdir /rootfs
```
```shell
mount /dev/block/mmcblk0p53 /rootfs
```
```shell
cd /external_sd
```
```shell
tar -xzpvf ubuntu-mate-18.04-rootfs.tar.gz -C /rootfs/
```
- Wait for it to finish
***Backup your LAF or BOOT partition***
```shell
dd if=/dev/block/bootdevice/by-name/laf of=/external_sd/laf-backup.img
```
(If you want to restore download mode later, 'dd' it back to the laf partition.)
- Flash the ubuntu boot image:
```shell
dd if=/external_sd/ubuntu-boot.img of=/dev/block/bootdevice/by-name/boot
```
To reboot into Ubuntu, completely turn off the phone, then hold volume up while plugging in the USB. You should see the download screen, then after about 15 seconds, youll see the login screen.

***For installing to SD card***
- Copy files to your internal storage
- Use the previous instructions but ***replace "mmcblk0p53" with "mmcblk1p1" and replace "/external_sd" with "/data/media/0"***
- Flash the "ubuntu-boot-sdcard.img" instead of "ubuntu-boot.img"
  
***TO LOGIN***
## Password: ***doital123***

Use a USB keyboard/mouse to easily navigate the system. Touch also works too. :)


