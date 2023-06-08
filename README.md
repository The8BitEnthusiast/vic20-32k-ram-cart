# A 32K RAM Expansion PCB and 3D Printed Cart for the VIC-20

![Splash](https://github.com/The8BitEnthusiast/vic20-32k-ram-cart/blob/main/pictures/pcb-3d.png?raw=true)

After building Ben Eater's 6502 breadboard computer, I undertook this project to see how hard it would be to upgrade the RAM of my VIC-20. After all, the VIC-20 is basically a BE6502 in a case with a video chip and a keyboard. This was also an opportunity to learn how expansion cartridges are designed.

## The Starting Point

I didn't want to start this project from scratch, so I looked around for prior designs. I eventually landed on this elegant [2-chip memory expansion design](http://www.zimmers.net/anonftp/pub/cbm/documents/projects/memory/vic20/32kB.html) from Adam Bergstrom. Absolutely brilliant. As the diagram below shows, there are 4 8K blocks of memory that are empty and available for expansion on the stock machine. There is also an additional 3K of RAM available, but I have opted to not exploit that so I stuck to a single 32K SRAM chip design.

![Memory Map](https://github.com/The8BitEnthusiast/vic20-32k-ram-cart/blob/main/pictures/memory-map-analysis.png?raw=true)

The diagram also shows how each available memory block is already decoded on the expansion port with 7 active-low chip select signals. 4 for each of the 8K blocks, and 3 for each 1K block in lower RAM. Adam's design exploits that by using a priority encoder, the 74LS147, to encode the chip-select lines into a 2-bit number that is fed to address pins A14 and A13 of the RAM chip. I had a 74LS148 priority encoder on hand, so I adjusted the design slightly to take into account the small differences.

## KiCAD Schematics

The schematics for the design is shown below. It is essentially a translation of Adam's design, with the minor modifications described above. For this project, one of my goals was to learn how to model an edge connector. As it happens, there is an excellent [tutorial for creating a C64 cartridge on Youtube](https://www.youtube.com/watch?v=8ikvcYKftms). All I had to do was adapt the specifications to the VIC-20 expansion port's pin pitch and dimensions. 

![Schematics](https://github.com/The8BitEnthusiast/vic20-32k-ram-cart/blob/main/pictures/schematics.png?raw=true)

## PCB Design

As I already had gained some exposure to PCB design through other tutorials, creating the PCB for this cartridge was relatively straighforward. The new knowledge I gained from the video tutorial referenced in the previous section was how to create a custom footprint. That was a great skill to acquire!

![PCB](https://github.com/The8BitEnthusiast/vic20-32k-ram-cart/blob/main/pictures/pcb-design.png?raw=true)

## Assembly

For this project I received some special brotherly help to get a cartridge shell 3D printed. The result was impressive, it was a precise match for the PCB!

![Assembly](https://github.com/The8BitEnthusiast/vic20-32k-ram-cart/blob/main/pictures/assembly.png?raw=true)

## Final Outcome

So there you have it, a homemade 32k ram expander. I plugged the cartridge in, and voilà, I was greeted with 28,159 bytes free, woohoo! ...now wait a minute (moment of panic), that's not 32K + 3, there is a whole 8K missing! After some research, I learned that memory is block 5 is not counted by Basic! All good, a few POKEs and PEEKs confirmed the availability of that 8K block!

![Outcome](https://github.com/The8BitEnthusiast/vic20-32k-ram-cart/blob/main/pictures/ram-diff.png?raw=true)
