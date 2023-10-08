# m17_tools

Development/research repo for M17 console


### Technical specs

- **CPU**: Rockchip RK3126C
- **RAM**: 256MB DDR3
- **Screen**: 4.3 inches 480x272
- **Ports**: USB-C power/data, headphone jack 3.5mm, microSD slot
- **Buttons**: volume +/-, power, gamepad buttons
- **Speaker**: 1 speaker


### Loader mode

Connect device to PC with USB cable, keep volume down button pressed, then power on the device.


### Recovery?? mode

Keep volume down pressed, power on the device. Stuck at Loading... screen, no interface through USB.


### ADB access

Place files under ADB folder on this repo on the root folder of your SD card. Turn on the device with SD card inserted, then connect with your computer and list adb devices.


### Root access

Root is the default user. Anything you include in em_ui.sh file under sdcard root folder will run as root (like the ADB-enabling script).


### Firmware backup

Using rkdeveloptool, rkloader or any other Rockchip-focused tool will only properly backup the first 32MB of flash, due to a bug? in device uboot. Anything beyond this point will be invalid data.
But as long as we have ADB shell and root permissions...

	dd if=/dev/mmcblk1 of=/sdcard/backup.img


### Emulationstation binaries

By default, an emulationstation binary on sdcard root is launched. Modifying em_ui.sh and pointing it to run "emulationstation" from system path instead of the sdcard path "/sdcard/emulationstation" will launch the binary present under /usr/bin, whose biggest difference is a new option under EmulationStation settings; Sound options.


### SD card booting

As long as you insert an SD card containing any compatible filesystem, device will try to boot from there instead of internal memory. No working example at this moment, but a good thing to know...


### Booting with no SD card

Booting device with no SD card inserted will display a basic emulator interface with some NES games. This happens when /sdcard/em_ui.sh script is not present, and /usr/bin/game is launched instead.


### Retroarch cores in userdata partition

In general, there is a lot of folders and files on SD card and system rootfs with no particular use or reason, probably things left from manufacturer tests. In this category we can find some roms and Retroarch cores under /userdata path. Cores can be manually launched, but they are prone to crash.
