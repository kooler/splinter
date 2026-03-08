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

## Building

### PCB
PCB is made to be ordered with assembly on JLCPCB. It contains Kailh switches, diodes and couple of 4.7 ohm resistors with references to respective components in JLCPCB. You might need to update those references if using another manufacturer, but for JLCPCB you can just upload the package and order the PCB. 

This is what you will receive:
![Splinter Keyboard PCB](https://github.com/kooler/splinter/blob/main/res/pcb.jpg?raw=true)


### Case
Print the STL files in `stl/` with 0.2mm layer height and 40% infill recommended.

## Bill of Materials

| Part | Quantity |
|------|----------|
| Pro Micro / Elite-C | 2 |

## License

Hardware design files (Gerbers, STLs, schematics) are licensed under  
[CC BY-NC-SA 4.0](LICENSE) © 2026 [Your Name]

✅ Personal builds allowed  
✅ Modifications allowed under the same license  
❌ Selling assembled keyboards or PCBs is not permitted
