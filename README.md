# RCA1802 ELF Build

## Scope

Record the construction of an COSMAC ELF clone. Install a monitor, BASIC and forth in EPROM.

## Introduction

The design chosen was created by Tor-Eirik Lunde, using the design files published on [github](https://github.com/tebl/RC1802-Cosmac-ELF). 
The PCB's were ordered via th shared community projects on PCBWay for the [CPU PCB](https://www.pcbway.com/project/shareproject/RC1802_Cosmac_ELF__CPU_module_revision_E_.html?inviteid=88707), [UI PCB](https://www.pcbway.com/project/shareproject/RC1802_Cosmac_ELF__UI_module_revision_E_.html?inviteid=88707) and {Backplnae PCB}(https://www.pcbway.com/project/shareproject/RC6502_Apple_1_Replica__Backplane_module_revision_A_.html).

Many of the IC's were purchased via a kit sold on eBay.
## Assembly

### CPU PCB

The CPU board is asembled with minor variations to allow for component availablity. In particlar the rectangular 1MHz oscilattor can was substituted with a square can version by mutilating some turned pin strip and bridging the pins underneath with soldered fine wire. 

Power was supplied via a common USB to serial converter. Ensure the jumper on the convert is set to supply 5V. The board volatege should be measured to be around 4.9 volts.

The main puzzle was getting the various jumpers set correcly for memory locations and serial communications.

### CPU Testing

The AT28C256 EEPROM was programmed with the loopback.hex file. This tests serial comminications by echoing keypresses om an attached PC. 

The Tera Term Windows aplication wa configured with settings Setup:Serial Port 600 baud, 8 bit. parity mark and 1 stop bit. 
![COM9 - Tera Term VT 12_01_2025 5_26_33 PM](https://github.com/user-attachments/assets/ac78f7d0-f8a7-40f6-b2cb-c1115c2d62a1)

The USB to serial converter was setup with 4 lines, Gnd, Rx, Tx and Vcc. The Rx and Tx lines crossover, so: Tx <--> Rx and Rx <--> Tx. This can be verifies by tapping a key and checking that the Tx LED on the converter flashes.

![CDP1802 serial connection](https://github.com/user-attachments/assets/dbf6cce9-fa8b-4102-9c05-0792b4163a77)


