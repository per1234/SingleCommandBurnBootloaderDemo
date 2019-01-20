### A demonstration of using a single avrdude command for the Arduino IDE's **Tools > Burn Bootloader** process
Normally, the AVR **Burn Bootloader** process happens in two `avrdude` commands:
1. "erase"
  - Erase flash (-e)
  - Set LOCKBIT fuse according to `bootloader.unlock_bits`.
  - Set EXTENDED fuse according to `bootloader.extended_fuses`.
  - Set HIGH fuse according to `bootloader.high_fuses`.
  - Set LOW fuse according to `bootloader.low_fuses`.
2. "bootloader"
  - Write bootloader file to flash.
  - Set LOCKBIT fuse according to `bootloader.lock_bits`.

The second `avrdude` command is run immediately after the first. When using the Atmel AVR Dragon or AVRISP mkII, this may be too quickly, which results in the failure of the second command `avrdude: usbdev_open(): did not find any USB device "usb"`.

`avrdude` will happily run the entire process described above in a single command with identical results. By moving the entire process to the "erase" command, then leaving the "bootloader" command empty, the problem with the Atmel programmers is resolved.

Note: This package includes a programmer definition for the AVR Dragon: **Tools > Programmer > AVR Dragon (Single Command Burn Bootloader)**.

References:
- https://github.com/arduino/Arduino/issues/650
- https://github.com/arduino/Arduino/issues/2986


#### Installation
There are two options for installing InoAVRDragon:
##### Boards Manager
This installation method requires Arduino IDE version 1.6.4 or newer.
1. Start the Arduino IDE.
1. **File > Preferences**
1. Enter the following URL in **Additional Boards Manager URLs**: https://per1234.github.io/SingleCommandBurnBootloaderDemo/package_per1234_SingleCommandBurnBootloaderDemo_index.json
    - If you already have a URL in that field, separate the URLs with a comma.
1. **Tools > Board > Boards Manager...**
1. Wait for the downloads to finish.
1. Scroll down until you see **SingleCommandBurnBootloaderDemo by per1234**. Click on it.
1. Click **Install**.
1. Wait for installation to finish.
1. Click **Close**.

##### Manual Installation
1. Download SingleCommandBurnBootloaderDemo from one of the **Source code** links of the newest release at: https://github.com/per1234/SingleCommandBurnBootloaderDemo/releases.
1. Extract the downloaded file.
1. Copy the extracted folder inside your sketchbook/hardware folder. You can find the location of the sketchbook folder in the Arduino IDE at **File > Preferences > Sketchbook Location**
1. If the Arduino IDE is running, restart it.
