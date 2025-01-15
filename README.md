# RCA1802 ELF Build

## Scope

Record the construction of an COSMAC ELF clone. Install a monitor, BASIC and forth in EPROM.

## Introduction

The design chosen was created by Tor-Eirik Lunde. I referred to the design files published on [github](https://github.com/tebl/RC1802-Cosmac-ELF). 
The PCB's were ordered via th shared community projects on PCBWay for the [CPU PCB](https://www.pcbway.com/project/shareproject/RC1802_Cosmac_ELF__CPU_module_revision_E_.html?inviteid=88707), [UI PCB](https://www.pcbway.com/project/shareproject/RC1802_Cosmac_ELF__UI_module_revision_E_.html?inviteid=88707) and [Backplnae PCB](https://www.pcbway.com/project/shareproject/RC6502_Apple_1_Replica__Backplane_module_revision_A_.html).

Many of the IC's were purchased via a kit sold on eBay. The kit is no longer available as far as I can tell, though individual components can be found.

## Assembly

### CPU PCB

The CPU board is asembled with minor variations to allow for component availablity. In particlar the rectangular 1MHz oscillator can was substituted with a square can version by mutilating some turned pin strip and bridging the pins underneath with soldered fine wire. 
![oscillator can mod](https://github.com/user-attachments/assets/b8bdb12a-2c62-495b-834b-8651e8762d8e)

Power was supplied via a common USB to serial converter. Ensure the jumper on the convert is set to supply 5V. The board volatege should be measured to be around 4.9 volts.

The main puzzle was getting the various jumpers set correcly for memory locations and serial communications. The memory map arbitrarily assigned the EPROM to slot 1 (nearest the CDP1802 chip) and the RAM to slot 2. The EPROM had write enable disabled (slot 1 WE), while the RAM has write enable enabled (slot 2 WE).

![memory map](https://github.com/user-attachments/assets/46a9924d-6826-4a16-9c2e-f648abba5d77)


### CPU Testing

For these tests to work, the /CLEAR pin on the microprocessor must be held high.
The CPU board does not provide a power on or manual reset circuit.
Consequently the code in EPROM will not execute reliably.
Execution of this code in indicated by illumination of the SCO LED.

Such a circuit was built on a spare connector with capacitor, resistor and normally open pushbutton switch.
This is then plugged into the CPU PCB as a temporary test fixture.

When the GUI daughter board is plugged in, it replaces the test fixture and this function is provided by the RUN switch. 
This may operate reliably without the RC circuit, until it does not.

#### Q Output Test

The AT28C256 EEPROM was programmed with the blink.hex file. This tests output from the Q pin on the microprocessor, by blinking around once per second.

The Q output can be monitored on the Tx invert/non-invert jumper, or by blinking of the Rx pin LED on the USB to serial converter.
Alternatively by monitoring a pin on the daughterboard connector or a pin on the backplane using an oscilloscope.

The LED on the daughter board flashes when Q is tested, when the daughter board is in place and the RUN switch is on.

#### Serial Communications Test

The AT28C256 EEPROM was programmed with the loopback.hex file. This tests serial comminications by echoing keypresses om an attached PC. 

The Tera Term Windows aplication wa configured with settings Setup:Serial Port 600 baud, 8 bit. parity mark and 1 stop bit. 
![COM9 - Tera Term VT 12_01_2025 5_26_33 PM](https://github.com/user-attachments/assets/ac78f7d0-f8a7-40f6-b2cb-c1115c2d62a1)

The USB to serial converter was setup with 4 lines, Gnd, Rx, Tx and Vcc. The Rx and Tx lines crossover, so: Tx <--> Rx and Rx <--> Tx. This can be verifies by tapping a key and checking that the Tx LED on the converter flashes.

![CDP1802 serial connection](https://github.com/user-attachments/assets/dbf6cce9-fa8b-4102-9c05-0792b4163a77)

The serial signal configuration jumpers were set for Rx non-invert (EF3), Tx invert (/Q)and Rx_select = EF3.

![Serial signal jumpers](https://github.com/user-attachments/assets/c72e4d6e-070c-4ffa-8966-7027a7afdc20)

