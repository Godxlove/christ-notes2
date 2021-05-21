When power initialized on system, execution starts at a fixed memory location
- Firmware ROM used to hold initial boot code


• Operating system must be made available to hardware so
hardware can start it
- Small piece of code – bootstrap loader, stored in ROM or EEPROM locates the kernel, loads it into memory,and starts it
- Sometimes two-step process where boot block at fixed location loaded by ROM code, which loads bootstrap loader from disk

• Common bootstrap loader, GRUB, allows selection of kernel from multiple disks, versions, kernel options
• Kernel loads and system is then running