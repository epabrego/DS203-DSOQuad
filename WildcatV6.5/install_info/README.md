INSTALLATION PROCEDURE:

1] Put DS203 into DFU (device firmware update) mode:
While power is down, press ">||" button, and while still holding this button down, power the device on

2] Connect DS203 to PC (using USB cable). New removable USB drive should appear on your PC

3a] Easy way - just copy the app1.hex file to that USB drive. After copying will finish, the USB drive should disappear briefly and reappear again and the extension of app1.hex will be changed to either .RDY (update successful) or .ERR (update NOT successful).
If you get .RDY, then just power off the device and that's it. At next power on, you'll boot to updated app.
If you get .ERR, try next step 3b].

3b] The hard way - sometimes / on newer devices with newer DFU version (V3.46C), the 3a] step will not work (on Windows it will stop in the middle of copying, reporting that it cannot access the drive and on Linux it will finish copying, but .ERR extension will appear).
I suspect that this is because this app is too big (for other smaller apps the 3a] is working ok).
Fortunately, there's another way how to update - copying raw binary .BIN files to that USB drive. But in binary files, there is no information to which address / memory location to copy that raw data. So the procedure is in reality to copy .ADR file first and then .BIN
.ADR files are plain text files, containing only one text line - 32-bit address in C-like hexadecimal format.
(example of .ADR file):
    0x0800C000
By doing this, we're telling to DFU that next .BIN file that will be copied should be written starting at that address.
So we just need to convert our app1.hex to app1.bin file, right?
    objcopy --input-target=ihex --output-target=binary app1.hex app1.bin
Well .. not so fast. If we do this, we'll overwrite other important data in flash memory! This is because the program code in app1.hex is not continuous. It's divided into 3 chunks that are on different locations in memory. By doing one .BIN, the gaps between program chunks will be stuffed by zeroes.
So what we need to do is to analyze the .HEX file and separate it into smaller .HEX files where program data are continuous. See IHEX format for details (https://en.wikipedia.org/wiki/Intel_HEX).
For this W6.5 version and app1.hex it will be:
    app1_a_addr_0800C000.hex
    app1_b_addr_0802C000.hex
    app1_c_addr_08047000.hex 
(I've done this manually in text editor. There's probably a way how to do similar thing using ARM GNU toolchain tools, but this was faster for me).
Then we'll convert to .BIN files:
    objcopy --input-target=ihex --output-target=binary app1_addr_0800C000.hex app1_a.bin
    objcopy --input-target=ihex --output-target=binary app1_addr_0802C000.hex app1_b.bin
    objcopy --input-target=ihex --output-target=binary app1_addr_08047000.hex app1_c.bin
And manually create .ADR files with proper addresses:
    app1_a.adr  <-- containing text "0x0800C000"
    app1_b.adr  <-- containing text "0x0802C000"
    app1_c.adr  <-- containing text "0x08047000"
OK! Now we're ready to update.
Copy files to DS203's USB drive (while DS203 in in DFU mode) in this order:
    app1_a.adr
    app1_a.hex
    app1_b.adr
    app1_b.hex
    app1_c.adr
    app1_c.hex

Tested on:
DS203 purchased on Dec-01 2017 via eBay
- HW ver. 2.82
- DFU: V3.46C
- SYS: ver. 1.64
- original APP: ver. 1.13
