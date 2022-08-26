# Bonsai C4

Brought to you by customMK, Bonsai C4 is an open source microcontroller board featuring an STM32F411CEU6 microcontroller. It is designed to be a drop-in-replacement for Proton C rev 2, Bonsai C, and Pro Micro. 

For a more compact version of Bonsai C4 that matches the length of a Pro Micro (for physical backwards compatibility reasons), please refer to Bonsai C4 compact edition found [here](https://github.com/customMK/Bonsai-C/tree/main/C4%20compact)

## Contents

- [Images](#images)
- [Pinout and DMA streams](#pinout-and-dma-streams)
- [Bonsai C4 and JLCPCB](#bonsai-c4-and-jlcpcb)
- [Usage in split keyboards](#usage-in-split-keyboards)
- [License](#license)

## Images

Bonsai C4 schematic
<img width="890" alt="Bonsai C schematic" src="https://raw.githubusercontent.com/customMK/Bonsai-C/main/C4/img/Bonsai%20C4%20schematic.png">
Bonsai C4 PCB front

<img width="200" alt="Bonsai C front" src="https://raw.githubusercontent.com/customMK/Bonsai-C/main/C4/img/Bonsai%20C4%20front.png">
Bonsai C4 PCB back

<img width="200" alt="Bonsai C back" src="https://raw.githubusercontent.com/customMK/Bonsai-C/main/C4/img/Bonsai%20C4%20back.png">

# Pinout and DMA streams

Detailed pinout information, peripherals available on each pin, and a DMA stream management utility (to avoid DMA conflicts) can be found [here](https://docs.google.com/spreadsheets/d/1FY-Vt8GbN7uX89lh9176jPXvGJELREzGpuhMts9ds38/edit?usp=sharing).

# Bonsai C4 and JLCPCB

The STM32F411CEU6 has a large thermal pad on the back that prevents signal vias and traces from being placed under the microcontroller. As such, it is challenging to route all the traces in a way that fits the original form factor of the ProMicro/Proton C/Bonsai C. To keep the same form factor, via-in-pad was necessary. For consistent results in PCB production, this ususaly means doing a non-conductive via fill, cap, and planarize operation, which JLCPCB does not do. 

While the JLCPCB process may not be ideal for such a layout, we have now successfully built and tested prototype of Bonsai C4 compact edition built by JLCPCB (March 2022) at a cost of around $35 per PCB for five PCBs. Some parts had to be swapped out, hole sizes were changes, and traces modified, but the files used to produce these JLCPCB can be found [here](https://github.com/customMK/Bonsai-C/tree/main/C4%20compact%20JLCPCB)

# Usage in split keyboards

Limitations the STM32F411CEU6 are of particular concern to designers of split keyboards. Specifially, due to design decisions by ST, it is difficult to support all possible USART_TX pin locations on a single PCB. To help overcome this issue, solder bridges have been provided that allow certain pins to be swapped. Using ProMicro pinout labeling as a reference, only D0, D1, D2, and D3 are supported for half duplex split communications. Without any modification to Bonsai C4, ProMicro D0 (as B6 on the STM32F411) and D2 (as A15 on the STM32F411) are supported for soft serial use.

There are two pairs of solder bridges on the back of the board. Cutting the traces between these solder bridges (e.g. with a razor blade/Exacto knife/etc.) and then soldering across the opposite pads will swap either the D0 and D1 pins, or the D2 and D3 pins (depending on which pair of solder bridges is being modified).

It should be noted that the default of assignment of STM32F411 A15 to ProMicro D2 was done intentionally, even though technically, as a USART TX pin, it seems like it should be wired to ProMicro D3 instead. The reason for this is that many more keyboards tend to use ProMicro D2 for half duplex soft serial communciations (as compared to those which use ProMicro D3). Unlike Atmega32U4 on the ProMicro, the STM32F411 can only use the USART TX pin for this purpose, so the USART TX pin (A14) has been wired to ProMicro D2. The solder bridge opposite the USB connector can be used to swap these back, but it seems better to support the more common use by default without requiring modification to the board.

# Split keyboard reset

Many split keyboard designs use the same PCB for left and right sides. This requires one of the microcontroller boards to be flipped over for installation, which makes the reset button inaccessible. A simple workaround is to un-solder the reset switch, and then solder it between the DFU and GND pins. Temporarily connecting DFU and GND performs the same function as the reset switch; specifically, it reboots the microcontroller into bootloader mode.


## License

Open sourced under the [CERN 2.0 permissive license](LICENSE.md).
