# Bonsai C

Brought to you by customMK, Bonsai C is an open source microcontroller board featuring an STM32F303CC microcontroller. Designed to be a drop-in-replacement for Proton C rev 2 (and thus also a replacment for Pro Micros). Bonsai C is functionally equivalent to the Proton C, while incorporating several design and manufactring improvements, including being "JLCPCB-ready" (aside from components being out-of-stock, which may happen occasionally...or in the case of the STM32F303CC, happens consistently).

# Bonsai C4

Bonsai C4 is also an open source microcontroller board featuring an STM32F411 microcontroller (because STM32F303CC has been unavailable for quite some time). Bonsai C4 is also designed to be a drop-in-repalcement for Pro Micros an Proton C. Aside from the hardware being usable in DIY keyboard kits, Bonsai C4 can serve as a useful reference and starting point for keyboards designer using STM32F411 becuase it incorporates the hardware necessary consistent USB DFU boot. More info on Bonsai C4 can be found [here](https://github.com/customMK/Bonsai-C/tree/main/C4)

Bonsai C4 is available in both a [compact edition](https://github.com/customMK/Bonsai-C/tree/main/C4) (same size as Pro Micro) and [extended edition] (https://github.com/customMK/Bonsai-C/tree/main/C4%20compact) (same size as Proton C). There is also a [JLCPCB-ready version of the compact edition](https://github.com/customMK/Bonsai-C/tree/main/C4%20compact%20JLCPCB), which meets hole size and trace/space requirements for JLCPCB

## Contents

- [Images](#images)
- [Background](#background)
- [Comparison to Proton C](#comparison-to-proton-c)
- [Build information](#build-information)
- [License](#license)


## Images

Bonsai C schematic

<img width="890" alt="Bonsai C schematic" src="https://user-images.githubusercontent.com/8145762/135368910-4f4df901-d462-4e76-adea-b27d1ca6e6b2.png">

Bonsai C fabricated by JLCPCB (disregard extra width, used to be JLCPCB requirement for 20mm minimum)

<img src="https://user-images.githubusercontent.com/8145762/135368388-da9367da-9e1b-4b06-abdc-4d8d9658e27e.jpg" width="200">

Bonsai C PCB front

<img width="200" alt="Bonsai C front" src="https://user-images.githubusercontent.com/8145762/135369024-da790e28-ae78-4fbe-8ac0-6569afe9ab0f.png">

Bonsai C PCB back

<img width="200" alt="Bonsai C back" src="https://user-images.githubusercontent.com/8145762/135369010-b38d721c-63c1-428b-8b84-19bf362b463b.png">

Bonsai C layers

<img width="200" alt="Bonsai C layers" src="https://user-images.githubusercontent.com/8145762/135368969-9ea1c17f-bcb1-4e4d-aa82-202842dbb81a.png">

## Background

Bonsai C is a general-purpose ARM-based microcontroller board. It was designed to help with the protoype and development of mechanical keyboards, but is versatile enough to be used in a variety of other applications. Mechanical keyboards can use Bonsai C as a "plug in" microcontroller board to their own designs sans-microcontroller, or they can incorporate the Bonsai C schmatic and layout directly into a complete keyboard PCB design.


## Comparison to Proton C

Bonsai C is designed to be a drop-in-replacement to Proton C, and as such, they are functionally equivalent. However, there are several subtle design differences in contrast to Proton C:

Bonsai C uses only parts in the JLCPCB SMT library (including the USB C connector)
Bonsai C’s USB data traces are shorter and more direct
Bonsai C's USB data traces are designed for the correct impedance, using a 4 layer board design with power and ground planes.
Bonsai C’s crystal clock lines are shorter and more direct
Bonsai C adds a ferrite between USB shield and ground, improving EMI (radiated susceptibility and radiated emissions)
Bonsai C connects USB VBUS to the ESD chip instead of the +5V (+5V is polyfuse-limited and reverse-diode-protected)
Bonsai C has correct labeling of the C14 and C15 pads (they are currently swapped in Proton C documentation and PCB silkscreen labeling)
Bonsai C uses ceramic bulk decoupling capacitors instead of tantalum capacitors
Bonsai C avoids via-in-pad (note: via-in-pad without non-conductive epoxy fill can cause solder joints to become starved of solder during assembly)

## Build information

Bonsai C is a four layer PCB design.

If you plan to fabricate the Bonsai C design "as-is" without modificiation, within the "build" folder are three different zip files to make it easier to achieve this:

<b>Bonsai_C_Gerbers_Only.zip</b> contains the Gerber files only. If you plan to solder parts on your own, you can simply take the zip file, send it to the PCB fab of your choice, and get boards made.

<b>Bonsai_C_PCBA.zip</b> has the set of files needed to make fully-assembled PCBs; this includes the Gerber files above as well as a BOM and position file for assembly. These files can be provided to most of PCB assembly shops when ordering fully assembled boards. Depending on the assembly shop, it may be necessary to use alternative parts for some of the passive components (depending on where components are sourced from) but these replacements .

Included are also JLCPCB-ready BOM and position files, so uploading the design can be done by simply uploading the Gerber zip, BOM file, and CPL file to JLCPCB. However, from time to time, parts may go in and out of stock without suitable replacements in the JLCPCB library, necessitating some tailoring and/or hand soldering of components.

To use the lower cost STM32F303CB microcontroller instead of STM32F303CC, simply edit the BOM file; the footprint is identical between the CC and CB variants.

If you are unable to source the microcontroller directly, keep in mind that with the right equipment (hot air rework station) it is possible to transplant microcontroller from other boards you may have. If you plan to program (and let end users reflash) the microcontroller over USB by using QMK Toolbox, you will want you select a microcontroller that includes an embedded USB bootloader, of which there are relatively few options to choose from:

![STM USB DFU](https://user-images.githubusercontent.com/8145762/135371363-8159e879-39a4-40b6-b926-7edc3be8aaf1.png)

See [here](https://github.com/qmk/qmk_firmware/issues/4194) for more information, particularly yiancar's comment on Oct 22, 2018. 

If you are willing to forego programming over the USB connector, and instead find it acceptable to use a low-cost SWD programmer (like ST-LINK) to flash new firmware onto the microcontroller, then there are many many more microcontroller options to choose from.

## License

Open sourced under the [CERN 2.0 permissive license](LICENSE.md).
