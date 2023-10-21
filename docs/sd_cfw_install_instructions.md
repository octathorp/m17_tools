# Ruka RK3128 Custom Firmware for M17 - Bootable SD

This is an adaptation/port of this original project: https://github.com/Ruka-CFW/rk3128-cfw

It's based on PS5000 version, modified and adapted for running on M17 hardware, so original features apply, surely a lot of new bugs also from my side.

### Installation

1.- Download SD release zip from [this repo Releases section.](https://github.com/octathorp/m17_tools/releases)

2.- Extract img file and write it on your SD. I personally recommend [balenaEtcher.](https://etcher.balena.io)

3.- Insert SD on your device and turn it on.

4.- You will be presented with the usual "Loading..." screen, then a new one with the text "Resizing SD card partitions, please wait", so please wait as it could take several minutes, depending on your SD.

5.- Once done, display will show Ruka CFW blue error screen. It's ok, turn off the device, extract the SD card and insert it in your PC.

6.- Copy the contents of the SD folder from the release zip under the "SHARE" partition. Make sure ".config" folder is copied also, as some systems could hide it.

7.- Extract your SD from the computer, insert on device and turn it on again.

8.- A new message, "Creating swap file, please wait" will show. Depending on your SD card, it could take between 10-15 minutes.

9.- Once done, Retroarch interface will be presented.

10.- Enjoy

### Things to note

- Screen brightness can be adjusted using L1 + Up/Down buttons
- This port has no support for running other systems inside a squashfs-format-rootfs placed on SD card. I could not build a proper loop.ko module for this kernel/device, so no chroot.
- This is more of a Proof-of-Concept than a serious project, I have used it to learn about this HW platform.
- There is a source-built, performance-oriented, profesionally-maintained system for this device coming soon, not from me for sure, so if you want something easy to set up and stable, then wait.
- But if you cannot wait and you like testing things... you are on your own.

### Future of this project

None, as stated above, it's just a PoC and an entertainment project, so I will not make improvements over it.
