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

1/30/15 update:
I've since picked up a Nu-Link-Pro programmer that should allow me to both see what is on the chip, and program it directly.  The hope is that I can decode the firmware format from Vortex using that.

TODO:
=====
1- Solder leads to my poker (Done!)

2- Use the Vortex tool to flash a known firmware file (Done)

3- Dump said firmware using the Nu-Link-Pro, compare the two firmware files to check for compatibility.  :: Apparently the Processor has a 'flash-lock' in place that prevents the tool from downloading firmware.  I'm going to try a USB Sniffer to see what actually gets written to the device.

4- If possible and necessary, write a tool to convert the 'dumped' to the Vortex tool format.  This would allow for programming WITHOUT the NU-Link, since the version on the chip would be in the 'programmed' state.

5- Begin custom firmware development!

5a- Start with getting IPS mode to work as closely to the Vortex version as possible, since hopefully this would allow us to reuse their tool to program the boards

5b- Attempt identification of keys on board and dip-switches

5c- write base version for key functionality

5d- LEDs? (difficult, since my board doesn't have LEDs installed, might have to solder them on).

5e- NKRO?

5f- More firmware functionality?  Programability?  Layers? etc?
