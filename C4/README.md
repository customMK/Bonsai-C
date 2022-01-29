# Bonsai C4

Brought to you by customMK, Bonsai C4 is an open source microcontroller board featuring an STM32F411CEU6 microcontroller. It is designed to be a drop-in-replacement for Proton C rev 2, Bonsai C, and Pro Micro. 

# Bonsai C4 and JLCPCB

The STM32F411CEU6 has a large thermal pad on the back that prevents signal vias and traces from being placed under the microcontroller. As such, it is challenging to route all the traces in a way that fits the original form factor of the ProMicro/Proton C/Bonsai C. To keep the same form factor, via-in-pad was necessary, as well as using smaller vias than JLCPCB can make. This means Bonsai C4 is not designed to accomodate JLCPCB. It still serves as a great reference design for keyboards however, which have much more generous space for trace routing.

# Bonsai C4 usage in split keyboards

Limitations the STM32F411CEU6 are of particular concern to designers of split keyboards. Specifially, due to design decisions by ST, it is difficult to support all possible USART_TX pin locations on a single PCB. To help overcome this issue, solder bridges have been provided that allow certain pins to be swapped. Using ProMicro pinout labeling as a reference, only D0, D1, D2, and D3 are supported for half duplex split communications. Without any modification to Bonsai C4, ProMicro D0 (as B6 on the STM32F411) and D3 (as A15 on the STM32F411) are supported. There are two pairs of solder bridges on the back of the board. Cutting the traces between these solder bridges (e.g. with a razor blade/Exacto knife/etc.) and then soldering across the opposite pads will swap either the D0 and D1 pins, or the D2 and D3 pins (depending on which pair of solder bridges is being modified).

## Contents

- [Images](#images)
- [License](#license)


## Images

Bonsai C schematic screenshot

<img width="890" alt="Bonsai C schematic" src="https://raw.githubusercontent.com/customMK/Bonsai-C/main/C4/img/Bonsai%20C4%20schematic.png">

Bonsai C PCB front

<img width="200" alt="Bonsai C front" src="https://raw.githubusercontent.com/customMK/Bonsai-C/main/C4/img/Bonsai%20C4%20front.png">

Bonsai C PCB back

<img width="200" alt="Bonsai C back" src="https://raw.githubusercontent.com/customMK/Bonsai-C/main/C4/img/Bonsai%20C4%20back.png">


## License

Open sourced under the [CERN 2.0 permissive license](LICENSE.md).
