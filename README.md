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
