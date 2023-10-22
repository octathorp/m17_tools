# Device recovery

To recover device from any issue while flashing or writing partitions I have put together a modified stock image capable of booting from SD card with ADB enabled by default. 

These instructions assume that you have a proper emmc backup.

### Follow this steps for a partition recovery (you flashed a wrong partition):

1.- Download m17_recovery.zip from [Releases section.](https://github.com/octathorp/m17_tools/releases)

2.- Extract img file and write it on your SD. I personally recommend [balenaEtcher.](https://etcher.balena.io)

3.- Insert SD on your device and turn it on.

4.- You will see the basic emulator interface, then connect device to your computer with an USB cable and make sure it is discoverable with "adb devices" command.

5.- You can extract partition images from your backup with tools like 7zip.

6.- Depending on the partition you need to recover, you must send the corresponding file via

    "adb push image_file /userdata/".

7.- Write back the image to partition with dd, "dd if=image_file of=/dev/mmcblk1pX", where X is the corresponding partition number:

    /dev/mmcblk1p1    uboot
    /dev/mmcblk1p2    trust
    /dev/mmcblk1p3    misc
    /dev/mmcblk1p4    boot
    /dev/mmcblk1p5    recovery
    /dev/mmcblk1p6    backup
    /dev/mmcblk1p7    oem
    /dev/mmcblk1p8    rootfs
    /dev/mmcblk1p9    userdata

8.- After performing any action you needed, run "sync" command to make sure everything has been properly written. Turn off the device, extract SD card and then turn it on again.


### Follow this steps for a full emmc recovery:

If you need to recover GPT and IDB (starting from sector 0) or your partition table is broken, then follow this steps:

1.- Connect device to PC. It should be detected as MaskRom (Rockchip emergency interface). If not, you could need to [short-circuit this test point with GND.](internal_interfaces.jpg)

2.- Use rkdeveloptool to load bootloader on memory (rk3126_bootloader_v2.09.bin on loader folder on this repo):

    rkdeveloptool db rk3126_bootloader_v2.09.bin

3.- Then restore your backup:

    rkflashtool w 0 7733248 <backup.img

4.- It will take a while. Once done, then run this command:

    rkflashtool b
