It doesn't matter if you have made a full backup of the device if when you have made a mistake you can't put the device in Loader mode to correct it.
That's what happens if you write the "uboot" partition with a corrupt or invalid file, since it seems to be the uboot itself the one in charge of activating that mode with the press of the corresponding button.

Therefore, if the "uboot" partition is corrupted, the device will not start the normal system, but it will not be able to go into Loader mode to be recovered either.

The logical solution was to use Maskrom mode to resurrect the device, but in the process there seems to be a special Loader file missing that I have not been able to locate anywhere. The header of the normal loader files starts with "RK31", while the necessary one should start with "BOOTf", so there was no way to load a loader in order to rewrite the corrupted partition.

Taking advantage of the ability of this device to boot from an SD if it is in the proper format, I recreated the logical structure that the embedded eMMC follows, so that it could boot from that SD. The genimage.cfg file I used is located in the "docs" folder of this repository.

Once this was done, I observed that the device booted properly, but in the basic "game" system, as there was no SD inserted with the rest of the content for Emulation Station.

Once that was done, I was able to verify that the rootfs that was mounted and in use was not the content on the SD, as I could disconnect the SD and the system was still running and able to load ROMs. My main idea was to modify the rootfs inside the SD to enable ADB by default, but that was not going to be able to happen.

In the end what worked was to power up the device with the SD recreated from the eMMC and when it loaded the uboot quickly swap the SD for another one containing Emulation Station and my script to enable ADB, so that with the full system booted I could access via ADB, send the original uboot.img to the SD and from the shell do:

    dd if=/sdcard/uboot.img of=/dev/mmcblk1p1

This way the uboot has been rewritten correctly and the device is back to normal.
