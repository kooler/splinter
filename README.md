# Splinter keyboard

A staggered 65% split keyboard.

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](LICENSE)

![Splinter Keyboard](https://github.com/kooler/splinter/blob/main/res/splinterkb-render.png?raw=true)


## Features

- 65% layout
- Hot-swap sockets

## Files

| File | Description |
|------|-------------|
| `gerber/` | PCB manufacturing files |
| `stl/` | 3D printable case and plate files |
| `firmware/` | QMK and ZMK firmware builds |

## Building

### PCB
PCB is made to be ordered with assembly on JLCPCB. It contains Kailh switches, diodes and couple of 4.7 ohm resistors with references to respective components in JLCPCB. You might need to update those references if using another manufacturer, but for JLCPCB you can just upload the package and order the PCB. 

This is what you will receive:
![Splinter Keyboard PCB](https://github.com/kooler/splinter/blob/main/res/pcb.jpg?raw=true)

Wired version of the keyboard runs on Pro Micro, for wireless I used nice!nano.

Besides those you'd need:
1. TRRS OR 4 pin JST connector PCB for connecting two halfs

PCB is made for this kind of PCB mounted audio jack port:
![Female trrs](https://github.com/kooler/splinter/blob/main/res/audio-jack.jpg.jpg?raw=true)
![Female trrs dimentions](https://github.com/kooler/splinter/blob/main/res/audio-jack-3.5mm-female-trrs-pj-313b-dimensions.jpg?raw=true)

or a JST-XH-4p 90 degree:
![JST-XH-4p](https://github.com/kooler/splinter/blob/main/res/jst-xh-4p.jpg?raw=true)

2. 2 x push buttons (optional) to make flashing easier:
![Push button](https://github.com/kooler/splinter/blob/main/res/pushbutton-4pin-6x6x6mm.jpg?raw=true)

For wireless you'd additionally need (and obviously don't need #1):
3. 2 x JST-PH-2p connectors for the battery connection:
![JST-PH-2p](https://github.com/kooler/splinter/blob/main/res/jst-ph-2p.jpg?raw=true)

4. 2 x lp503035 battery
![battery](https://github.com/kooler/splinter/blob/main/res/lp503035.jpg?raw=true)

5. 2 x mini rocker switch for turning each side on/off
![rocker switch](https://github.com/kooler/splinter/blob/main/res/rocker-switch.jpg?raw=true)

##### Soldering

Soldering the PCB is a bit tricky as we'd need the Pro mini or nice!nano headers to be mega short so that buttons can be placed on the other side of the PCB on top of them.

The controller is soldered on the back of the board above Kailh switches. To make life easier I would suggest to use this kind of pins that have a small spacer in between the board and the PCB: 
![pin headers](https://github.com/kooler/splinter/blob/main/res/headers-2.54mm-40p.jpg?raw=true)

if you don't want to solder the controller directly to the PCB you could also use a female headers like this and then insert the headers with spacer into them. It will work but will obviously take more space:
![reusing controller](https://github.com/kooler/splinter/blob/main/res/reusable-controller.jpg?raw=true)
![reusing controller with controller](https://github.com/kooler/splinter/blob/main/res/reusable-controller2.jpg?raw=true)

Once you have controller with pin header, insert it into board, it will look something like this:
![board-before](https://github.com/kooler/splinter/blob/main/res/board-before.jpg?raw=true)

*VERY IMPORTANT:* Before doing next step: USE EYE PROTECTION! Those tiny pin ends fly like little bullets and one of them might (and will) hit your eyes. So protect them!

we'd need to shave those pins so that they are not sticking from the PCB because otherwise the switch will not be able to sit on top of them. Just use a flush cutter tool:
![tool](https://github.com/kooler/splinter/blob/main/res/tool.jpg?raw=true)

*VERY IMPORTANT:* USE EYE PROTECTION!

Just cut them one by one. You'd want to endup with something like this:
![board after cut](https://github.com/kooler/splinter/blob/main/res/board-after-cut.jpg?raw=true)

Now it's ready to be soldered. After soldering the controller, on the same side solder TRRS/JST4 or battery JST connectors. All those goes to the back of the board.
![board after soldered](https://github.com/kooler/splinter/blob/main/res/board-after-soldered.jpg?raw=true)

That's it for soldering. Now check the firmware section below.

### Firmware
#### QMK

While the PR to the official QMK is being reviewed you can use my fork to build the firmware: https://github.com/kooler/qmk_firmware

##### Without VIA support
```sh
# compile
qmk compile -kb splinter/65/rev1 -km default
# flash left
qmk flash -kb splinter/65/rev1 -km default -bl avrdude-split-left
# flash right
qmk flash -kb splinter/65/rev1 -km default -bl avrdude-split-right
```

##### With VIA support
```sh
# compile
qmk compile -kb splinter/65/rev1 -km default -e VIA_ENABLE=yes
# flash left
qmk flash -kb splinter/65/rev1 -km default -e VIA_ENABLE=yes -bl avrdude-split-left
# flash right
qmk flash -kb splinter/65/rev1 -km default -e VIA_ENABLE=yes -bl avrdude-split-right
```

You can also use prebuild binaries in `firmware/`.

### Case
Print the STL files in `stl/` with 0.2mm layer height and 40% infill recommended.

## License

Hardware design files (Gerbers, STLs, schematics) are licensed under  
[CC BY-NC-SA 4.0](LICENSE) © 2026 [Your Name]

✅ Personal builds allowed  
✅ Modifications allowed under the same license  
❌ Selling assembled keyboards or PCBs is not permitted
