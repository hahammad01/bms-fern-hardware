# Battery Management System Hardware — Formula Electric Racing NUST

Two PCBs from the accumulator monitoring system of the Formula Electric Racing
NUST (FERN) electric race car: a slave board that measures cell voltages and
temperatures across a high-voltage pack, and a temperature-sensing board shaped
to slot between cell modules.

Both were designed, fabricated, assembled and brought up for the 2023
competition car. FERN placed **1st in Asia and 22nd of over 100 teams at Formula
Student UK 2023**.


---

## BMS Slave Board

`Rev 1.0 · 352.9 × 92.6 mm · 2-layer`

Monitors one segment of the accumulator: 21 cell taps, 7 temperature channels
and a current shunt input, with isolated communication to the master and a
shutdown output to the tractive system.

**Measurement.** Two cascaded `CD74HC4067` 16-channel analogue multiplexers
reduce every input to a single line, digitised by an **`ADS1220` 24-bit
delta-sigma ADC** over SPI. An Arduino Nano sequences the multiplexers, reads
the ADC and runs the fault logic.

**Isolation.** Every crossing of the HV/LV boundary is galvanically isolated —
an `ISO1540` for I²C, a `CYPC817` optocoupler for the shutdown signal, and an
isolated 90 V → 5 V converter for board power. The HV and LV zones are marked on
the silkscreen with a high-voltage warning symbol at the boundary.

**Shutdown chain.** The optocoupler drives a MOSFET chain — two `IRF540N` into
an `IRF5305` high-side switch — producing the signal that opens the tractive
system on a fault. Green and red status LEDs report board state at a glance
inside the accumulator.

[Schematic, 8 sheets](BMS%20Board/BMS%20-%20Schematic.pdf) ·
[Layout](BMS%20Board/BMS%20-%20PCB.png) ·
[Assembled](BMS%20Board/IMG_3991.JPG.jpeg)

![BMS slave board layout](BMS%20Board/BMS%20-%20PCB.png)

![BMS slave boards installed in the accumulator](BMS%20Board/IMG_3991.JPG.jpeg)

---

## Temperature Sensing Board

`Rev 1.0 · 141.1 × 129.9 mm · 2-layer`

A comb-shaped board whose fingers slot down between cell modules so that the
thermistors sit against the cells. The outline is dimensioned to the pack
geometry — finger pitch, length and web width are mechanical constraints.

**Sensing.** Each channel is an NTC thermistor in a divider with a 10 kΩ
resistor, buffered by an `LM324` quad op-amp. A chain of `SN74LVC2G53` dual
analogue switches then multiplexes the channels onto a single line, so the whole
board returns to the BMS slave over one signal wire plus power rather than one
wire per sensor.

[Schematic](Temperature%20PCB/Temperature%20sensing%20-%20Schematic.pdf) ·
[Layout](Temperature%20PCB/Temperature%20sensing%20-%20PCB.png) ·
[Assembled](Temperature%20PCB/Temperature%20sensing.jpg)

![Temperature sensing board layout](Temperature%20PCB/Temperature%20sensing%20-%20PCB.png)

![Temperature sensing board installed against the cells](Temperature%20PCB/Temperature%20sensing.jpg)

---

## Not included

Firmware, Gerber and drill files, the BOM and the EasyEDA project sources are
not published. This repository exists to show design work.

## Safety

These boards form part of a high-voltage battery management system operating at
pack potential. They are published here as a record of past design work. They
are not a validated reference design and carry no safety certification. Do not
build from, adapt or rely on this material for any high-voltage or battery
system.

## Licence

**All rights reserved.** Published for portfolio review only. No permission is
granted to copy, modify, manufacture or redistribute this material. This work
was produced as a member of the Formula Electric Racing NUST team, so rights in
the design are not held solely by the author.

## Attribution

Designed by **Muhammad Hammad Hassan Mallick** — Senior Member, Controls and
Battery Management and **Hammad Safeer"** - Lead, Controls and
Battery Management , Formula Electric Racing NUST.

The accumulator and the wider vehicle were the work of the full FERN team.
