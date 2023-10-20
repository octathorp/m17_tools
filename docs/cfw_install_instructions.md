# Ruka RK3128 Custom Firmware for M17

This is an adaptation/port of this original project: https://github.com/Ruka-CFW/rk3128-cfw

It's based on PS5000 version, modified and adapted for running on M17 hardware, so original features apply, surely a lot of new bugs also from my side.

### Warnings

Installing this will overwrite stock system. Unless you restore original rootfs partition after installing this, you will not be able to run original system again.
This is not a SD-only installation. 

We are not aware of different hardware revisions, but being an obscure device anything can happen. Make sure you have a device emmc backup.

Do not use this if you don't understand these warnings.

### Installation

1.- Make sure you have a device backup, as explained in [Readme.](https://github.com/octathorp/m17_tools/blob/master/README.md)

2.- Download zip from [this repo Releases section.](https://github.com/octathorp/m17_tools/releases)

3.- Unpack it, write rootfs.img in Loader mode with your preferred RK tool [I'm using rkdeveloptool fork from Pine64.](https://gitlab.com/pine64-org/quartz-bsp/rkdeveloptool)

4.- Place content from SD folder on your FAT32 format SD card.

5.- Insert your SD, turn on device and wait.

6.- System is creating a swapfile under userdata partition, so it will remain at "Loading..." screen for several minutes.

7.- After that, Retroarch main menu will be presented.

8.- Enjoy.

### Things to note

- Screen brightness can be adjusted using L1 + Up/Down buttons
- This port has no support for running other systems inside a squashfs-format-rootfs placed on SD card. I could not build a proper loop.ko module for this kernel/device, so no chroot.
- This is more of a Proof-of-Concept than a serious project, I have used it to learn about this HW platform.
- There is a source-built, performance-oriented, profesionally-maintained system for this device coming soon, not from me for sure, so if you want something easy to set up and stable, then wait.
- But if you cannot wait and you like testing things... you are on your own.

### Future of this project

None, as stated above, it's just a PoC and an entertainment project, so I will not make improvements over it.
