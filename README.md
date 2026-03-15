# Splinter keyboard

A staggered 65% split keyboard.

<a href="LICENSE"><img src="https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg" alt="License: CC BY-NC-SA 4.0"/></a>

<img src="https://github.com/kooler/splinter/blob/main/res/splinterkb-render.png?raw=true" alt="Splinter Keyboard"/>


## Features

- 65% layout
- Hot-swap sockets
- Wired or wireless option

## Files

| File | Description |
|------|-------------|
| `gerber/` | PCB manufacturing files |
| `step/` | 3D printable case and plate files |
| `firmware/` | QMK and ZMK firmware builds |

## Building

### PCB
PCB is made to be ordered with assembly on JLCPCB. It contains Kailh sockets, diodes and couple of 4.7 ohm resistors with references to respective components in JLCPCB. You might need to update those references if using another manufacturer, but for JLCPCB you can just upload the package and order the PCB. 

This is what you will receive:
<img src="https://github.com/kooler/splinter/blob/main/res/pcb.jpg?raw=true" alt="Splinter Keyboard PCB"/>

Wired version of the keyboard runs on Pro Micro, for wireless I used nice!nano.

#### Components

##### 1. TRRS OR 4 pin JST connector PCB for connecting two halves (wired only) 

Two halves can be connected either via TRRS cable or JST-XH-4p cable. 

**IMPORTANT:** If using TRRS do not connect both halves while the keyboard is powered to avoid shorting it.

The following TRRS connector is supported:

<img src="https://github.com/kooler/splinter/blob/main/res/audio-jack.jpg?raw=true" height=200 alt="Female TRRS"/><img src="https://github.com/kooler/splinter/blob/main/res/audio-jack-3.5mm-female-trrs-pj-313b-dimensions.jpg?raw=true" alt="Female TRRS dimensions" height=200/>

or a JST-XH-4p 90 degree:

<img src="https://github.com/kooler/splinter/blob/main/res/jst-xh-4p.jpg?raw=true" alt="JST-XH-4p" height=200/>

##### 2. 2 x push buttons to make flashing easier

Optional, you can also short two pins if not planning to flash that too often. 

<img src="https://github.com/kooler/splinter/blob/main/res/pushbutton-4pin-6x6x6mm.jpg?raw=true" alt="Push button" height=200/>

##### 3. 2 x JST-PH-2p connectors for the battery connection (wireless only) 

<img src="https://github.com/kooler/splinter/blob/main/res/jst-ph-2p.jpg?raw=true" alt="JST-PH-2p" height=200/>

##### 4. 2 x lp503035 battery (wireless only) 

<img src="https://github.com/kooler/splinter/blob/main/res/lp503035.jpg?raw=true" alt="battery" height=200/>

##### 5. 2 x mini rocker switch for turning each side on/off (wireless only) 

<img src="https://github.com/kooler/splinter/blob/main/res/rocker-switch.jpg?raw=true" alt="rocker switch" height=200/>

#### Soldering

Soldering the PCB is a bit tricky as we'd need the Pro Micro or nice!nano headers to be mega short so that switches can be placed on the other side of the PCB on top of them.

The controller is soldered on the back of the board above Kailh sockets. To make life easier I would suggest to use this kind of pins that have a small spacer in between the board and the PCB: 

<img src="https://github.com/kooler/splinter/blob/main/res/headers-2.54mm-40p.jpg?raw=true" alt="pin headers" height=200/>

if you don't want to solder the controller directly to the PCB you could also use a female headers like this and then insert the headers with spacer into them. It will work but will obviously take more space:

<img src="https://github.com/kooler/splinter/blob/main/res/reusable_controller.jpg?raw=true" alt="reusing controller" height=200/>
<img src="https://github.com/kooler/splinter/blob/main/res/reusable_controller2.jpg?raw=true" alt="reusing controller with controller" height=200/>

Once you have pin headers soldered to the controller, insert it into the board, it will look something like this:

<img src="https://github.com/kooler/splinter/blob/main/res/board-before.jpg?raw=true" alt="board-before" height=200/>

**VERY IMPORTANT:** Before doing next step: USE EYE PROTECTION! 

Now we'd need to shave those pins so that they are not sticking from the PCB because otherwise the switch will not be able to sit on top of them. Just use a flush cutter tool:

<img src="https://github.com/kooler/splinter/blob/main/res/tool.jpg?raw=true" alt="tool" height=200/>

**VERY IMPORTANT:** REALLY, USE EYE PROTECTION! Those tiny pin ends fly like little bullets and one of them might (and will) hit your eyes. So protect them!

Just cut them one by one. You'd want to end up with something like this:

<img src="https://github.com/kooler/splinter/blob/main/res/board-after-cut.jpg?raw=true" alt="board after cut" height=200/>

Now it's ready to be soldered. After soldering the controller, on the same side solder TRRS/JST4 or battery JST connectors. All those go to the back of the board.

<img src="https://github.com/kooler/splinter/blob/main/res/board-after-soldered.jpg?raw=true" alt="board after soldered" height=200/>

After that solder the reset push button (if you are adding it) and rocker switch for wireless version.

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

You can also use prebuilt binaries in `firmware/`.

#### ZMK

ZMK Firmware available in this repo: https://github.com/kooler/splinter-zmk

### Case
The simple case can be completely 3rd printed, it contains two parts for each side and uses m2 inserts and bolts for connection.

<img src="https://github.com/kooler/splinter/blob/main/res/case.jpeg?raw=true" alt="3d printed case components" height=200/>

Print the STEP files in `step/`.

If you'd like to design you own, in step folder you can find step file with PCB and components, so that you can design your case around it.

## License

Hardware design files (Gerbers, STEPs, schematics) are licensed under  
[CC BY-NC-SA 4.0](LICENSE) © 2026 [SplinterKB]

✅ Personal builds allowed  
✅ Modifications allowed under the same license  
❌ Selling assembled keyboards or PCBs is not permitted
