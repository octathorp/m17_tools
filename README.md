# m17_tools

Development/research repo for M17 console


### Technical specs

- **CPU**: Rockchip RK3126C
- **RAM**: 256MB DDR3
- **Screen**: 4.3 inches 480x272
- **Ports**: USB-C power/data, headphone jack 3.5mm, microSD slot
- **Buttons**: volume +/-, power, gamepad buttons
- **Speaker**: 1 speaker


### Custom firmware (RukaCFW Retroarch)

[Read more here](https://github.com/octathorp/m17_tools/blob/master/docs/cfw_install_instructions.md)


### Default system structure

Factory system is installed within this partition scheme:

	NO  LBA       Name                
	00  00004000  uboot
	01  00006000  trust
	02  00008000  misc
	03  0000A000  boot
	04  0001A000  recovery
	05  0002A000  backup
	06  0003A000  oem
	07  00102000  rootfs
	08  00202000  userdata

- uboot and trust follow RK norm
- misc, backup and oem partitions are empty
- boot and recovery are Android-scheme boot images. boot has no ramdisk included, recovery seems to not be used in a normal boot process.
- rootfs contains a custom-built Buildroot Linux system. Using an script at /etc/init.d, em_ui.sh is launched if it's located under SD card mount point, otherwise /usr/bin/game is launched.
- userdata, despite being mounted, seems to not be used at the current stage.

SD card contains default "emulationstation" binary, config files and ROMs, but whole system is installed on internal memory.


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


### EmulationStation Settings

Both "emulationstation" binaries present on this system have been built without normal user settings integrated (on code), so there is no way of "unlocking" options through es_settings.xml or similar methods.


### SD card booting

As long as you insert an SD card containing any compatible filesystem, device will try to boot from there instead of internal memory. No working example at this moment, but a good thing to know...


### Booting with no SD card

Booting device with no SD card inserted will display a basic emulator interface with some NES games. This happens when /sdcard/em_ui.sh script is not present, and /usr/bin/game is launched instead.


### Retroarch cores in userdata partition

In general, there is a lot of folders and files on SD card and system rootfs with no particular use or reason, probably things left from manufacturer tests. In this category we can find some roms and Retroarch cores under /userdata path. Cores can be manually launched, but they are prone to crash.


### Running other systems on M17

~~Technically there are no limitations on running another system on this device, as long as someone takes the time to make a port for this platform. Internal flash is writable using rkdeveloptool or even Rockchip proprietary tools, and we have a proper backup of the original content. So given the similarity of this system to Powkiddy A12/A13 or PS5000, that should be the way to go.~~

[You could give a try to this, no guarantees](docs/cfw_install_instructions.md)


### UART interface

[Three points indicated, square one is GND](docs/internal_interfaces.jpg)


### Force Maskrom mode

[Short circuit this test point with GND](docs/internal_interfaces.jpg)


### Debugging with UART while booting from SD card

It's impossible, as some CPU bus is shared between UART and SD card, so logging text is corrupted with SD card activity electrical noise...


### Recovering from a bad flash

[Device recovery with a SD bootable image](docs/device_recovery.md)

[My first experience recovering this device, do not follow this procedure](docs/Recovering-from-a-bad-flash.md)
