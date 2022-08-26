# Bonsai C3

## Contents

- [Images](#images)
- [Background](#background)
- [Comparison to Proton C](#comparison-to-proton-c)
- [Build information](#build-information)
- [License](#license)


## Images

Bonsai C3 schematic

<img width="890" alt="Bonsai C3 schematic" src="https://user-images.githubusercontent.com/8145762/135368910-4f4df901-d462-4e76-adea-b27d1ca6e6b2.png">

Bonsai C3 fabricated by JLCPCB (disregard the extra width, 20mm minimum width used to be JLCPCB requirement)

<img src="https://user-images.githubusercontent.com/8145762/135368388-da9367da-9e1b-4b06-abdc-4d8d9658e27e.jpg" width="200">

Bonsai C3 PCB front

<img width="200" alt="Bonsai C3 front" src="https://user-images.githubusercontent.com/8145762/135369024-da790e28-ae78-4fbe-8ac0-6569afe9ab0f.png">

Bonsai C3 PCB back

<img width="200" alt="Bonsai C3 back" src="https://user-images.githubusercontent.com/8145762/135369010-b38d721c-63c1-428b-8b84-19bf362b463b.png">

Bonsai C3 layers

<img width="200" alt="Bonsai C3 layers" src="https://user-images.githubusercontent.com/8145762/135368969-9ea1c17f-bcb1-4e4d-aa82-202842dbb81a.png">

## Background

Bonsai C3 is a general-purpose ARM-based microcontroller board. It was designed to help with the protoype and development of mechanical keyboards, but is versatile enough to be used in a variety of other applications. Mechanical keyboards can use Bonsai C3 as a "plug in" microcontroller board to their own designs sans-microcontroller, or they can incorporate the Bonsai C schmatic and layout directly into a complete keyboard PCB design.


## Comparison to Proton C

Bonsai C3 is designed to be a drop-in-replacement to Proton C, and as such, they are functionally equivalent. However, there are several subtle design differences in contrast to Proton C:

<ul>
  <li>Bonsai C3 uses only parts in the JLCPCB SMT library (including the USB C connector)</li>
  <li>Bonsai C3’s USB data traces are shorter and more direct</li>
  <li>Bonsai C3's USB data traces are designed for the correct impedance, using a 4 layer board design with power and ground planes.</li>
  <li>Bonsai C3’s crystal clock lines are shorter and more direct</li>
  <li>Bonsai C3 adds a ferrite between USB shield and ground, improving EMI (radiated susceptibility and radiated emissions)</li>
  <li>Bonsai C3 connects USB VBUS to the ESD chip instead of the +5V (+5V is polyfuse-limited and reverse-diode-protected)</li>
  <li>Bonsai C3 has correct labeling of the C14 and C15 pads (they are currently swapped in Proton C documentation and PCB silkscreen labeling)</li>
  <li>Bonsai C3 uses ceramic bulk decoupling capacitors instead of tantalum capacitors</li>
  <li>Bonsai C3 avoids via-in-pad (note: via-in-pad without non-conductive epoxy fill can cause solder joints to become starved of solder during assembly)</li>
</ul>

## Build information

Bonsai C3 is a four layer PCB design.

If you plan to fabricate the Bonsai C3 design "as-is" without modificiation, within the "build" folder are two different zip files to make it easier to achieve this:
<ul>
<li><b>Bonsai_C3_Gerbers_Only.zip</b> contains the Gerber files only. If you plan to solder parts on your own, you can simply take the zip file, send it to the PCB fab of your choice, and get boards made.</li>

<li><b>Bonsai_C3_PCBA.zip</b> has the set of files needed to make fully-assembled PCBs; this includes the Gerber files above as well as a BOM and position file for assembly. These files can be provided to most of PCB assembly shops when ordering fully assembled boards. Depending on the assembly shop, it may be necessary to use alternative parts for some of the passive components (depending on where components are sourced from).</li>
</ul>
Included are also JLCPCB-ready BOM and position files, so uploading the design can be done by simply uploading the Gerber zip, BOM file, and CPL file to JLCPCB. However, from time to time, parts may go in and out of stock without suitable replacements in the JLCPCB library, necessitating some tailoring and/or hand soldering of components.

To use the lower cost STM32F303CB microcontroller instead of STM32F303CC, simply edit the BOM file; the footprint is identical between the CC and CB variants.

If you are unable to source the microcontroller directly, keep in mind that with the right equipment (hot air rework station) it is possible to transplant microcontroller from other boards you may have. If you plan to program (and let end users reflash) the microcontroller over USB by using QMK Toolbox, you will want you select a microcontroller that includes an embedded USB bootloader, of which there are relatively few options to choose from:

![STM USB DFU](https://user-images.githubusercontent.com/8145762/135371363-8159e879-39a4-40b6-b926-7edc3be8aaf1.png)

See [here](https://github.com/qmk/qmk_firmware/issues/4194) for more information, particularly yiancar's comment on Oct 22, 2018. 

If you are willing to forego programming over the USB connector, and instead find it acceptable to use a low-cost SWD programmer (like ST-LINK) to flash new firmware onto the microcontroller, then there are many many more microcontroller options to choose from.

## License

Open sourced under the [CERN 2.0 permissive license](LICENSE.md).
