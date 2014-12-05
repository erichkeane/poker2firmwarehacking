poker2firmwarehacking
=====================
KBC/Vortex Poker 2 Mechanical Keyboard Firmware hacking

Flash tool and firmware files can be found attached to this post: https://geekhack.org/index.php?topic=50245.0

Brief debugging/firmware file decoding has been done here: 

http://reverseengineering.stackexchange.com/questions/5945/finding-the-actual-thumb-code-in-firmware

Seemingly doing this decodes the firmware:
rotate left 4 bits and invert:  
c = (((c & 0x0f) << 4) | ((c & 0xf0) >> 4)) ^ 0xff

Processor is an ARM Cortex-M0 in a NUC122SC1AN:

http://www.nuvoton.com/hq/products/microcontrollers/arm-cortex-m0-mcus/nuc120-122-123-220-usb-series/nuc122sc1an/?__locale=en

"Valid" code seems to begin at 0x120.  Header is potentially everything before that, Footer is the last 16 bytes.  Last 4 bytes look to be some sort of checksum.


TODO:
=====
1- Decode binary file format
2- Create 'base' firmware that can be used as a starting point for customization


