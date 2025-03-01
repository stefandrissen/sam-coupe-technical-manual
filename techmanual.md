### Miles Gordon Technology plc

# SAM Coupé Technical Manual

### version 3.0

(C) 1990

The purpose of this manual is to introduce hardware and software developers to the internal and external workings of the SAM Coupé computer. To this end it is a technical document assuming a certain amount of technical knowledge.

It is MGT's policy that the SAM Coupé and associated MGT products should be fully documented to help third party software and hardware developers take full advantage of all the Coupé's advanced features. If you are developing a product for the Coupé and require further clarification or explanation MGT technical staff will be pleased to assist.

All production machines contain ROM 1.0. This manual details information for ROM 1.0 and ROM 1.2. In the period April/May 1990 all Coupé owners will be issued with an enhanced ROM, issue 2.0, free of charge. The ROM 1.2 referred to in this manual is a pre-production version of ROM 2.0.

- written by
Bruce Gordon a Andy Wright

- With additional information by
Gary Thomas & Adrian Parker

- Supplementary information on the use of the SAA1099 sound chip
by Andy Graharn

- With special Thanks to
Bob Brenchley, Simon Goodwin, W. Ettrick Thomson, and Nev Young

While every effort has been made to ensure that the contents of this manual are correct in every particular, it must be appreciated that MGT cannot guarantee that it is definitive since we have a policy of continual product enhancement.

- Published by Miles Gordon Technology plc
- Century Park Valley Way Swansea SA6 8QP
- Tel: 0792 791100 Fax: 0792 791175

### TECHNICAL SUPPORT FOR PROFESSIONAL DEVELOPERS

More and more hardware and software developers are working on SAM Coupé products.

MGT is keen to support the efforts of developers. To this end we have created the MGT SAM Coupé Developers Group. For a fee of £50.00 we offer members of the Developers Group the following benefits:

- Unlimited telephone support from our Software Engineers.
- Unlimited telephone support from our Hardware Engineers.
- Free and first-off-the-press updates to the Technical Manual.
- Free copies of supplementary information provided by developers, (where permission to distribute such information has been given).
- Hardware port address allocation for hardware developers. This will avoid the possibility of two devices Using the same port address(es).

- SAM Compatible: if a product, hardware or software, works with the Coupé we can issue 'SAM Compatible' stickers for the product case or packaging.

- Developers Group registration number to ensure priority service.

If you require further information, or wish to join the Developers Group, please either write to, or phone, our Technical Department whose staff will be pleased to help you.

# Contents

## [The SAM Coupé hardware](#the-sam-coupé-hardware-1)

### [General Specifications](#general-specifications-1)

### [Interfaces](#interfaces-1)
- [MIDI In](#midi-in)
- [MIDI Out](#midi-out)
- [Break (NMI) Button](#break-nmi-button)
- [Joystick](#joystick)
- [Mouse Port](#mouse-port)
- [Reset Button](#reset-button)
- [Cassette Jack](#cassette-jack)
- [Light Pen & Audio Port](#light-pen--audio-port)
- [Power Input](#power-input)
- [Euroconnector (Expansion Connector)](#euroconnector-expansion-connector)
- [SCART Socket](#scart-socket)
- [UHF Output](#uhf-output)
- [Slimline Slot-In Disk Drives](#slimline-slot-in-disk-drives)
- [Disk Drive Interface](#disk-drive-interface)

### [Memory](#memory-2)
- [Introduction](#introduction-1)

### [Screen Modes](#screen-modes-1)
- [Introduction](#introduction-2)
- [Mode 1](#mode-1)
- [Mode 2](#mode-2)
- [Mode 3](#mode-3)
- [Mode 4](#mode-4)
- [Locating The Current Screen](#locating-the-current-screen)

### [Keyboard](#keyboard-1)

### [Input/Output Ports](#inputoutput-ports-1)
- [Write (Output) Ports](#write-output-ports)
- [Read (Input) Ports](#read-input-ports)

### [Philips SAA1099 Sound Chip](#philips-saa1099-sound-chip-1)
- [Introduction](#introduction-3)
- [Noise & Sound](#noise--sound)
- [Pitch](#pitch)
- [Music](#music)
- [The Chromatic Scale](#the-chromatic-scale)
- [Octave Registers](#octave-registers)
- [Amplitude Registers](#amplitude-registers)
- [Noise Generators](#noise-generators)
- [Envelope Registers](#envelope-registers)

## [The SAM Coupé Software](#the-sam-coupé-software-1)

### [Memory](#memory-3)
- [SAM Coupé Memory Map](#sam-coupé-memory-map)
- [Screen Memory Location](#screen-memory-location)
- [The Stack](#the-stack)

### [ROM](#rom-1)
- [Use Of ROM Subroutines](#use-of-rom-subroutines)
- [Using Screen Modes 3 & 4](#using-screen-modes-3-and-4)
- [Palette Switching](#palette-switching)
- [The Paging System](#the-paging-system)
- [ROM Resources (Jump Table)](#rom-resources)
- [Character Set](#character-set)
- [Vectors](#vectors)

### [Floating Point Calculator Command Codes](#floating-point-calculator-command-codes-1)

### [Tape System](#tape-system-1)
- [File Header Format](#file-header-format)

## [SAM BASIC](#sam-basic-1)

### [BASIC/Machine Code Interface](#basic--machine-code-interface)

### [Major Pointers To BASICs Memory Area](#major-pointers-to-basics-memory-area-1)
- [Page Allocation Table](#page-allocation-table)
- [Keyboard](#keyboard-2)
- [Streams & Channels](#streams--channels)
- [Sound](#sound)
- [Graphics Scaling System](#graphics-scaling-system)

### [Keyword Codes](#keyword-codes-1)

### [System Variables](#system-variables-1)

### [Variable Formats](#variable-formats-1)
- [Format Of A Basic Program](#format-of-a-basic-program)

## [The SAM Coupé Disk Operating System](#sam-coupé-disk-operating-system)

### [Introduction](#introduction-4)
- [Disk Drives](#disk-drive)
- [Disk Format](#disk-format)

### [Disk File Header](#disk-file-header-1)
- [File Types](#file-type)
- [Modulo Length & Number Of Pages](#modulo-length--number-of-pages)
- [Offset Start & Starting Page Number](#offset-start--starting-page-number)
- [SAMDOS Directory](#samdos-directory)
- [Sector Address Map](#sector-address-map)
- [Bit Address Map](#bit-address-map-bam)

### [SAMDOS Interfacing](#samdos-interfacing-1)
- [User Information File Area (UIFA)](#user-information-file-area-uifa)
- [SAMDOS Hook Codes](#samdos-hook-codes)
- [Locating SAMDOS](#locating-samdos)
- [SAMDOS Error Codes](#samdos-error-codes)

### Appendix A: Philips SAA1099 Sound Chip
### Appendix B: VLSI VL-1772-02 Floppy Disk Controller Chip
### Appendix C: Diagrams

### [Stop Press](#stop-press-1)

# The SAM Coupé Hardware

The SAM Coupé is a modern micro-computer using a Z80B microprocessor running at 6MHz. It has 256K RAM as standard, with an expansion socket to allow the memory to be doubled to 512K with a small expansion board.

The machine's main controller is a VLSI VGT-200 gate array (ASIC), customised to carry out the main tasks of processor/video contention, paging and management of all memory, video memory mapping, colour palette table allocation, and all input/output port control. There are
four modes of video operation with a hardware capacity to show 16 colours from a palette of 128 on each screen line.

The sound for the machine is generated by a Philips SAA1099, with a capability in stereo of six channels over eight octaves with 256 tones per octave, two white noise generators, six amplitude controllers and two envelope wave shapers.

# General Specifications

|             ||
|-------------|---------------------------------
| CPU         | Z80B microprocessor running at 6MHz
| Special     | Customised VLSI 10,000-gate ASIC chip
| ROM         | 32K x 8 ROM, 150nS, containing SAM BASIC, disk bootstrap, BIOS
| RAM         | 256K upgradeable to 512K (256K x 4 100ns DRAM)
| Sound       | Philips SAA 1099 Synthesizer: 6 channels, 8 octaves, stereo with amplitude and envelope control, plus choice of wave form.
| Graphics    | Motorola MC 1377P Video Chip. ASIC serves as graphics processor, offering four modes: <ol> <li> Mode 1 32 x 24 character cells per screen, each cell  capable of 2 colours; 16 colours selectable from 128; Spectrum-attribute compatible. <li> Mode 2 As mode 1, but with 32 x 192 cells, each cell capable of 2 colours: 16 colours selectable from 128. <li> Mode 3 80 column text display - 512 x 192 pixel screen; each pixel selectable for colour; 4 colours per line selectable from 128. <li> Mode 4 256 x 192 pixel graphics screen; each pixel selectable for colour; 16 colours selectable per line from 128. </ol> In all modes, colours may be redefined at line interrupt, allowing all 128 colours to be displayed on-screen.
| TV          | UHF (TV channel 36), through power supply unit. Colour composite video, digital and linear RGB, all through SCART.
| Joystick    | Atari-standard joystick (dual capability with splitter cable).
| Mouse       | Coupé standard.
| Light-pen, <br> Light-gun | Coupé standard.
|             | Audio output socket.
|             | Domestic cassette recorder.
| MIDI        | MIDI In, MIDI Out (MIDI Through, via software switch).
| Network     | screened microphone cable with 7 pin DIN connectors.
| Comms       | RS232 and parallel printer via external MGT interface connected at expansion port.
| Expansion   | 64-pin Euroconnector for further peripherals.
| Disk Drives | 1 or 2 removable and internally mounted 3.5” ultra-slim Citizen drives, 1 Mb unformatted, 780K formatted.
| Keyboard    | 72 full travel keys, membrane type, including 10 function keys (software defined).

Power Consumption 11.2 Watts.

Shock
- Operating 3 G
- Non-operating 60 G

Vibration
- Operating 5 - 500Hz / 0.5 G
- Non-operating 5 - 500Hz / 2 G

Environmental: Ambient Temperature
- Operating 5 - 45 C
- Storage -20 - 50 C

Relative Humidity
- Operating 20 - 80%
- Wet Bulb Maximum 29.4 C, No Condensation

Reliability:
- MTBF: 10,000 POH; MTTR: 30 Mins;
- Component Life: >5 years

Weight
- 2.26Kg (4.97 lb)

Power Supply
- Primary Input voltage 240v AC 50Hz
- Secondary Output voltage 5v DC 2A Maximum Rating / 12v DC 200mA Maximum Rating

# Interfaces

All connections to the Coupé except the removable internal disk drives, and the RAM expansion socket are made via the rear panel. Please refer to the Input/Output Port map where reference is made to bits and registers.

## MIDI In

Standard 7 pin DIN type connector. This serial input, working at 31.25 Kbaud is fed via an opto-isolator to a serial/parallel converter, which interrupts the CPU when a data byte has been assembled in the MIDI-IN register (253 dec). This INPUT can also be read by bit 7 of the
Video Memory Page Register VMPR (252 dec). This connector is also used by the network.

| Pin | Signal
|-----|------------
| 1   | NET - LOOP
| 2   | N.C.
| 3   | NET + LOOP
| 4   | MIDI + IN
| 5   | MIDI - IN
| 6   | NET - LOOP
| 7   | NET + LOOP

## MIDI Out

Standard 7 pin DIN type connector. By writing a data byte to the MIDI-OUT register (253 dec), the MIDI outputs a 7.5 mA current at 31.25 Kbaud. when transmitting, bit 1 of the PEN register (TXFMST of register 248 dec), is set. This OUTPUT can also be driven by bit 7 of the VMPR (252 dec). An internal through connection is made from MIDI IN to OUT by setting bit 6 THROM (through MIDI) of the BORDER register (254 dec). This connector is also used by the network, An interrupt is given on completion of the transmission of MIDI data.

| Pin | Signal
|-----|------------
| 1   | NET - LOOP
| 2   | GND.
| 3   | NET + LOOP
| 4   | MIDI + OUT
| 5   | MIDI - OUT
| 6   | NET - LOOP
| 7   | NET + LOOP

## Break (NMI) Button

When pressed, this button forces the CPU to address (0066H) where it is vectored to any assignable address in the memory map. A versatile function for programmers to assign a vector, to enable its use as an ESC, BREAK or CRASH key. When the Disk Operating System Spectrum Emulator is loaded this button is used to activate the Snapshot facility.

## Joystick

Standard 9 pin 'D' type plug. The joystick interface has standard ATARI connections except that it has an extra strobe line for a second joystick together with a line carrying 5 volts. MGT will allow for dual joystick control with the second joystick having a special plug-socket connector. The joystick is read by the Keyboard port (254 dec) and overlays numeric keys 1 to 5 for second joystick and 6 to 0 for the first joystick.

| Pin | Signal
|-----|----------
| 1   | UP
| 2   | DOWN
| 3   | LEFT
| 4   | RIGHT
| 5   | 0 VOLTS
| 6   | FIRE
| 7   | +5 VOLTS
| 8   | STROBEL 1
| 9   | STROBEL 2

## Mouse Port

Proprietary 8 pin DIN type connector. The MGT mouse interrupts the CPU to request a read of its X and Y signal lines. The software driver is integral to the ROM and overlays the cursor control keys. The mouse input can be read by Keyboard port (254 dec) with address lines A8 to
A15 set high. (RDMSEL).

| Pin    | Signal
|--------|--------
| 1      | DOWN
| 2      | UP
| 3      | CTRL
| 4      | LEFT
| 5      | RIGHT
| 6      | MSE INT.
| 7      | RDMSEL
| 8      | +5 VOLTS
| SCREEN | GROUND.

## Reset Button

When pressed this button causes the CPU to clear and restart at memory location (0000H). It also resets the following:

1. Floppy Disk Controller (Disk 1 and 2)
2. Memory page registers
3. MIDI receive and transmit registers
4. Border register

It does not reset the colour look up table, the sound chip registers or the LINE INTerupt register (249 dec) value. The ROM normally initialises LINE INT as part of its initialisation.

## Cassette Jack

Standard 3.5mm mono jack socket. This is a bi-directional line. when outputting it should be connected to the MIC socket of a standard cassette tape recorder; when inputting it should be connected to the EAR socket of the recorder. It makes no difference to the Coupé if EAR and MIC are connected together, but only some tape recorders allow this, because of positive feedback.

## Light Pen & Audio Port

Standard 5-pin, 180 degree, DIN type connector. This connector has a dual function of light-pen/gun input as well as stereo sound output capable at driving a HI-FI system on the AUX input.

| Pin | Signal
|-----|----------
| 1   | +5 VOLTS
| 2   | AUDIO LEFT OUTPUT
| 3   | 0 VOLTS
| 4   | SPEN INPUT
| 5   | AUDIO RIGHT OUTPUT

## Power Input

Regulated DC input of 12 Volts at 200 milliamps and 5 Volts at 2 Amps. A fully loaded machine will have a power consumption of approximately 15 watts.

| Pin | Signal
|-----|----------
| 1   | +5 VOLTS
| 2   | 0 VOLTS (SIGNAL GROUND)
| 3   | 0 VOLTS (DIGITAL GROUND)
| 4   | COMPOSITE VIDEO
| 5   | +12 VOLTS
| 6   | SOUND OUTPUT (MONO)

## Euroconnector (Expansion Connector)

The Coupé's Euroconnector is a standard 64 pin type with rows A-C fitted. It has all the typical hardware signals found on other computer expansion ports. In addition, we include many extra hardware signals on the connector. This allows the hardware designer a hitherto unknown flexibility and control of a microcomputer from an external device.

### Signals

(NB row A is at the bottom of the Euroconnector, row C at the top).

| Pin | Signal   | Pin | Signal
|-----|----------|-----|-
| 1A  | DBDIR    | 1C  | IORQL
| 2A  | RDL      | 2C  | MREQL
| 3A  | WRL      | 3C  | HALTL
| 4A  | BUSAKL   | 4C  | NMIL
| 5A  | WAITL    | 5C  | INTL
| 6A  | BUSREQL  | 6C  | CD1
| 7A  | RESETL   | 7C  | CD0
| 8A  | CM1L     | 8C  | CD7
| 9A  | REFRESHL | 9C  | CD2
| 10A | 0 VOLTS  | 10C | +5 VOLTS
| 11A | A0       | 11C | CD6
| 12A | A1       | 12C | CD5
| 13A | A2       | 13C | CD3
| 14A | A3       | 14C | CD4
| 15A | A4       | 15C | CPU CLK
| 16A | A5       | 16C | A15
| 17A | A6       | 17C | A14
| 18A | A7       | 18C | A13
| 19A | A8       | 19C | A12
| 20A | A9       | 20C | A11
| 21A | A10      | 21C | DISK 2L
| 22A | MSEINTL  | 22C | ROMCSL
| 23A | XMEML    | 23C | EARMIC
| 24A | 8 MHz    | 24C | DISK 1L
| 25A | RED 1    | 25C | PRINTL
| 26A | GREEN 1  | 26C | BLUE 1
| 27A | C SYNC   | 27C | ROMCSRL
| 28A | SPEN     | 28C | AUDIO RIGHT OUTPUT
| 29A | BLUE 0   | 29C | AUDIO LEFT OUTPUT
| 30A | RED 0    | 30C | COMP VIDEO
| 31A | BRIGHT   | 31C | GREEN 0
| 32A | +5 VOLTS | 32C | 0 VOLTS

when looking at the back of the Coupé's expansion connector, the pins are numbered as follows:

| Euroconnector ||
|--------|---------
| Pin 1C | Pin 32C
| Pin 1A | Pin 32A

For details of Z80B timing signals refer to any standard Z80 text. Please note that we will be releasing the SAM Coupé Multi Expansion (SME) in the near future. (This product has been referred to as the Card Cage in some of our literature). Some of the signals described here must be included in any designs to ensure their correct operation when used with the SME.

|            |     ||
|------------|-----|-
| DBDIR      |  1A | This signal is not used by the computer but must be driven by all external devices to allow their use with the SME. The SME has buffers present to prevent undue loading of the machine. However, it is the responsibility of the hardware designer to ensure that the data bus transceiver has its direction bit set according to the operation (read or write) being performed. The operation should be as follows:<ol><li>Processor sends out an address.<li>External device decodes address.<li>External device drives the DBDIR line, from an open collector output, LOW for a processor READ. It is configured as a WIRED-OR internally to the computer.<li>Normal handshaking is continued with the Z80B for data transfer.</ol>
| RDL        |  2A | Read signal from the processor.
| WRL        |  3A | Write signal from the processor.
| BUSAKL     |  4A | Bus acknowledge signal from the processor.
| WAITL      |  5A | Wait signal to processor.
| BUSREQL    |  6A | Bus request signal to external device.
| RESETL     |  7A | This is a system reset generated by a 10 Kilohm resistor charging a 47 microfarad capacitor. This gives a pulse of approximately 330ms duration. It is suggested that if a sharp reset edge is required, this signal is passed through a Schmitt inverter.
| CM1L       |  8A | Op-code fetch signal from the processor
| REFRESHL   |  9A | Refresh signal from the processor.
| 0 V        | 10A | Zero Volt: not to be used as a supply rail.
| A0         | 11A | Address lines A0 to A10 from the processor are on pins 11A to 21A.
| MSEINTL    | 22A | Mouse interrupt signal also present on the mouse port. The signal is pulled low by an external device to notify the processor that the mouse co-ordinates have changed.
| XMEML      | 23A | External memory signal which will be driven low when the processor requires to switch out the internal memory and access the external memory. Please note that only memory above address 8000H in each block of 64K will be switched out. It is the responsibility of the peripheral designer to ensure that the XMEM signal is included in the address decoding circuitry of the design, to avoid contention between the internal RAM and the external device.
| 8MHZ       | 24A | 8 MegaHertz clock signal.
| RED1       | 25A | Each colour is generated by three colour driver signals, the intensity of which is determined by three bits each. RED1 is the MSB (Most Significant Bit) of the red colour signal at the current pixel position.
| GREEN1     | 26A | GREEN1 is the MSB of the green colour signal (see pin 25A for a full description).
| CSYNC      | 27A | Composite Sync for video circuitry as on the SCART connector.
| SPEN       | 28A | Light pen signal (active high) which is normally low. When the light pen is touched to the screen and the raster passes the point of the pen, a positive going edge is received on this signal from the light pen socket. This causes the two registers LPEN and HPEN to contain the current x and y co-ordinates of the light pen, respectively.
| BLUE0      | 29A | BLUE0 is the second bit of the blue colour signal (see pin 25A for a full description).
| RED0       | 30A | RED0 is the second bit of the red colour signal (see pin 25A for a full description).
BRIGHT       | 31A | BRIGHT is the LSB (Least Significant Bit) of all colour signals (see pin 25A for a full description).
| +5V        | 32A | +5 Volt supply rail, up to 250 mA available.
|            |     |
| IORQL      |  1C | Input/Output Request becomes active when the address bus contains a current port address from the processor.
| MREQL      |  2C | Memory Request becomes active when the address bus contains a current memory address from the processor.
| HALTL      |  3C | Halt indicates from the processor that it has executed a HALT instruction and is waiting for an interrupt.
| NMIL       |  4C | Non Maskable Interrupt causes the processor to execute a jump, from which it may be vectored anywhere by the user. It is used as a BREAK button by BASIC, and a SNAPSHOT button by the DOS. It is pulled up by a 10 Kilohm resistor internally, and should therefore be driven low by an open collector circuit.
| INTL       |  5C | Maskable Interrupt is used to interrupt the processor from its current task if the interrupts are currently enabled.
| CD1        |  6C | Data lines D1,D0,D7 and D2 are on pins 6C to 9C.
| +5V        | 10C | +5 Volt reference only.
| CD6        | 11C | Data lines D6,D5,D3 and D4 are on pins 11C to 14C.
| CPUCLK     | 15C | The 6 MegaHertz clock signal to the processor.
| A15        | 16C | Address lines A15 to A11 are on pins 16C to 20C.
| DISK2L     | 21C | DISK2 is the decoded base address for the eight ports of drive 2.
| ROMCSL     | 22C | ROM chip select is pulled high to disable the internal ROM (Used in conjunction with ROMCSR on pin 27C) It indicates when the ROM is being accessed.
| EARMIC     | 23C | EARMIC is connected to the logic level side of the cassette port circuitry.
| DISK1L     | 24C | DISK1 is the decoded base address for the eight ports of drive 1.
| PRINTL     | 25C | PRINT is the decoded address for either of the two possible printer addresses (246 and 248).
| BLUE1      | 26C | BLUE1 is the MSB of the blue colour signal (see pin 25A for a full description).
| ROMCSRL    | 27C | ROMCSR is connected to the ROMCS (22C) pin via a 1 Kilohm resistor. If ROMCS is pulled high by an external circuit, then ROMCSR could be used as a chip select for an external ROM which would then take the place on the internal one.
| AUDIORIGHT | 28C |The right audio signal, as on the light pen socket, is brought out here. (50mV pp as per auxiliary standard input) It must be amplified before being applied to a speaker.
| AUDIOLEFT  | 29C | The left audio signal is present on this pin. The same precautions and signal levels as for AUDIORIGHT apply.
| CVID       | 30C | Composite Video, as sent to the modulator and SCART socket is present on this pin.
| GREEN0     | 31C | GREEN0 is the second bit of the green colour signal (see pin 25A for a full description).
| 0 V        | 32C | Zero Volt supply rail.

## SCART Socket

SCART socket to handle all video and sound outputs. **Please note that not all connections are standard.**

| Pin | Signal
|-----|---------
|  1  | AUDIO OUT RH
|  2  | SPEN
|  3  | AUDIO OUT LH
|  4  | AUDIO EARTH
|  5  | BLUE EARTH
|  6  | BLUE TTL OUT
|  7  | BLUE LIN. OUT
|  8  | RED TTL OUT
|  9  | GREEN EARTH
| 10  | GREEN TTL OUT
| 11  | GREEN LIN. OUT
| 12  | +5V POWER IN
| 13  | RED EARTH
| 14  | CSYNC EARTH
| 15  | RED LIN. OUT
| 16  | CSYNC
| 17  | C.VID EARTH
| 18  | +12V POWER IN
| 19  | C.VID OUT
| 20  | BRIGHT TTL OUT
| 21  | GND.

## UHF Output

UHF television standard video and mono sound are output on channel 36; the UHF output is in the power supply box.

## Slimline Slot-In Disk Drives

The disk drives used in the SAM Coupé are Citizen Slim Line OSDC type 3.5", 1 megabyte (formatted 780 kilobytes).

The Coupé can control up to two disk drives. Connections to the two drives are made via two 32-pin Euroconnectors, with rows A and B connected. Drive 1 is on the left of the machine and drive 2 on the right. A list of signals available at these sockets are shown below.

| Pin | Signal  | Pin | Signal
|-----|---------|-----|---------
|  1A | 0 VOLTS |  1B | WR
|  2A | 0 VOLTS |  2B | A0
|  3A | 0 VOLTS |  3B | A1
|  4A | 0 VOLTS |  4B | D0
|  5A | 0 VOLTS |  5B | D1
|  6A | 0 VOLTS |  6B | D2
|  7A | 0 VOLTS |  7B | D3
|  8A | 0 VOLTS |  8B | D4
|  9A | 0 VOLTS |  9B | D5
| 10A | 0 VOLTS | 10B | D6
| 11A | 5 VOLTS | 11B | D7
| 12A | 5 VOLTS | 12B | 8 MHz
| 13A | 5 VOLTS | 13B | RST
| 14A | 5 VOLTS | 14B | No connection
| 15A | 5 VOLTS | 15B | A2
| 16A | 5 VOLTS | 16B | DISK 1 OR DISK 2

## Disk Drive Interface

The SAM Coupé can be connected to one or two disk drives. These would normally be internal SAM disk drives. However, we have made provision for people to use an external disk drive, (Shugart 400 type 5.25" or 3.5"), if they add the SAM External Drive Interface (SDI). Both the internal drives and the SDI use the VL-1772-02 disk controller chip manufactured by VLSI.

NB All values are given in Decimal.

The SAM Coupé controls each disk drive via 8 I/O mapped ports, as listed below for both drives:

- Disk 1 224 to 231 inclusive.
- Disk 2 240 to 247 inclusive.

In each case, the address can be given by:

- Disk1base (224) + offset (0 to 7)
- Disk2base (240) + offset (0 to 7)

Both sets of offsets perform the same functions on their respective sides of the disk. The first four offsets (0-3) refer to the first side of the disk, and the second four offsets, (4-7) refer to the second side of the disk. Offsets 4-7 can be ignored for single sided disk drives.

The offset determines which register of the 1772 will be accessed as shown below:

| Offset | Read   | Disk Side | Write   | Disk Side
|--------|--------|-----------|---------|-----------
| 0      | Status | 1         | Command | 1
| 1      | Track  | 1         | Track   | 1
| 2      | Sector | 1         | Sector  | 1
| 3      | Data   | 1         | Data    | 1
| 4      | status | 2         | Command | 2
| 5      | Track  | 2         | Track   | 2
| 6      | Sector | 2         | Sector  | 2
| 7      | Data   | 2         | Data    | 2

For example, to read the current contents of the data register on side 2 of Disk 1:

``IN A,(231)``

where 231 = Disk1base (224) + offset (7)

For complete information on controlling the 1772 chip refer to the data sheets contained in Appendix B.

# Memory

## Introduction

The Coupé can take 512 Kbytes of RAM on board (with extra memory able to be added via the expansion connector using signal XMEML). The basic machine has 256Kb fitted, with an internal expansion connector for an additional 256Kb. The memory used is Dynamic Random Access Memory 256K x 4 bits - 100nS access time, 20 pin dual in-line plastic package.

Because the Z80B CPU (central Processing Unit) is limited to a 64K addressing range, one of the functions of the ASIC (Application Specific Integrated Circuit) in the Coupé is to manage the addressing of this memory by splitting it into 32 pages of 16K.

The ASIC controls the paging via two 8-bit read/write registers.

- LMPR (Low  Memory Page Register)...I/O address 250dec
- HMPR (High Memory Page Register)...I/O address 251dec

The lower 5 bits of each register represent pages 0 to 31. (Of course on the basic machine with 256K of memory fitted, the paging is from 0 to 15).

To illustrate the paging system used by the Coupé, it's best to envisage the 64K addressing range of the Z80 as 2 blocks of 2 sections of 16K, represented by the letters A.B and C.D:


````
  |<--------- 64K ADDRESS RANGE --------->|

0000      4000      8000      C000       FFFF
  +---------------------------------------+
  | SECTION | SECTION | SECTION | SECTION |
  |    A    |    B    |    C    |    D    |
  +---------------------------------------+
   \    BLOCK A.B    / \    BLOCK C.D    /
 ````

LMPR manages the block A.B, and the HMPR manages the block C.D

If we write 00H to the LMPR then page 0 of the memory is allocated to section A of the CPU address range. Section B is always automatically allocated one page above section A, in this case to page 1.

If we write 02H to the HMPR then page 2 of the memory is allocated to section C of the CPU address range. Section D is always automatically allocated one page above section C, in this case to page 3.

In our example the CPU address map would look like this:

````
  |<--------- 64K ADDRESS RANGE --------->|

0000      4000      8000      C000       FFFF
  +---------------------------------------+
  | PAGE 0  | PAGE 1  | PAGE 2  | PAGE 3  |
  |    A    |    B    |    C    |    D    |
  +---------------------------------------+
   \    BLOCK A.B    / \    BLOCK C.D    /
 ````

# Screen Modes

## Introduction

There are four screen modes used in the Coupé, each using varying amounts of memory and each having different attributes for use by the programmer.

The hardware pointers which display the contents of the memory are controlled by the VMPR, Video Memory Page Register (252 dec).

By using the lower 5 bits of this register we can access up to 32 pages of video screen memory. It must be noted that modes 3 and 4 use 24 kilobytes, which go over the page boundary of 16 kilobytes. Where this happens, the video addressing hardware wraps into the next page within the same block. For example:

By entering page 12 to the VMPR, video wraps to page 13

The same applies to any page and the principal of even to odd always applies.

## Mode 1

32 cells x 24 lines in 2 colours from 16 out of a palette of 128 colours, giving 768 character cells (8 x 8) using 6 kilobytes of bitmapped memory and 0.75 kilobytes of attribute memory. This mode emulates Spectrum memory mapping.

## Mode 2

32 cells x 192 lines in 2 colours from 16 out of a palette of 128 colours, giving 6144 character cells (8 x 1) using 6 kilobytes of bitmapped memory and 6 kilobytes of attribute memory. This mode has contiguous memory addressing in two blocks.

## Mode 3

512 pixels x 192 lines in 4 colours out of a palette of 128 colours, giving 98304 dots using 24 kilobytes of memory. This mode, when used with a character set 6 pixels wide, will give 85 characters per line.

## Mode 4

256 pixels x 192 lines in 16 colours out of a palette of 128 colours, giving 49152 dots using 24 kilobytes of memory. This mode is ideal for graphic display, and when used in conjunction with LINE INTerrupt register can display the full 128 colours on screen.

## Locating The Current Screen

The SAM Coupé provides a port called Video Memory Page Register (address 252). To locate the base address of the currently displayed screen use the following BASIC program:

````
10 LET A=IN 252 BAND 31     REM Input the current page
20 LET BASE=(A+1) * 16384   REM BASE now equals start of screen area.
````

# Keyboard

The Coupé has a full-travel 72 key keyboard. It is addressed as a 9 x 8 matrix, using two ports, KEYBOARD (254 dec) and STATUS (249 dec).

The 8 input lines are made up by the KEYBOARD port inputting the lower 5 bits represented by K1, K2, K3, K4 and K5, while the STATUS port inputs the upper 3 bits represented by K6, K7 and K8.

The 9 output scan lines are made up by the CPU address lines AD8, AD9, AD10, AD11, AD12, AD13, AD14, AD15 and the ASIC line RDMSEL.

An example of a typical keyboard scan:

````
    ld hl,scan          ; set HL with buffer start
    ld b,11111110bin    ; set upper address lines

loop:
    ld c,HiKey          ; port address K6 - K8
    in a,(c)
    and 11100000bin     ; strip unwanted bits
    ld (hl),a           ; hold it

    ld c,LoKey          ; port address K1 - K5
    in a,(c)
    and 00011111bin     ; strip unwanted bits
    or (hl)             ; make K1 - K8
    ld (hl),a           ; save it

    inc hl              ; next location in buffer
    scf                 ; set carry flag for
    rlc b               ; rotate next address line
    jr c,loop           ; jump if not done

    in a,(c)            ; input RDMSEL line
    and 00011111bin     ; strip unwanted bits
    ld (hl),a           ; save it

    ret                 ; return to analyse scan
````

# Input/Output Ports

The SAM Coupé can address 64k of ports. Addresses 224 (E0H) to 255 (FFH) are allocated to the Coupé itself. Refer to the diagram provided for an overview of these ports and their contents.

## Write (Output) Ports

**SOUND** ports (address port 511 dec) and (data port 255 dec)

The sound chip, a Philips SAA1099, is controlled through these two port addresses. The sound chip is controlled in BASIC through using the ``SOUND a,d`` command. See the attached Philips application notes and the SAA1099 supplements included elsewhere for further information.

**VMPR** - Video Memory Page Register (252 dec)

This read/ write register mainly controls the page addressing for the screen display memory.

| Bit | R/W |        ||
|-----|-----|--------|------------------------
| 0   | R/W | BCD 1  | of video page control.
| 1   | R/W | BCD 2  | of video page control.
| 2   | R/W | BCD 4  | of video page control.
| 3   | R/W | BCD 8  | of video page control.
| 4   | R/W | BCD 16 | of video bank control, used to switch between the banks of 256 kilobytes.
| 5   | R/W | MDE0   | first bit of screen mode control.
| 6   | R/W | MDE1   | second bit of screen mode control.
| 7   | -/W | TXMIDI | output bit to directly drive the MIDI OUT channel.
| 7   | R/- | RXMIDI | input bit from MIDI IN channel.

**HMPR** - High Memory Page Register (251 dec)

This read/write register is used mainly for the control of paging memory in the CPU's addressing range.

| Bit | R/W |        ||
|-----|-----|--------|------------------------------
| 0   | R/W | BCD 1  | of high memory page control.
| 1   | R/W | BCD 2  | of high memory page control.
| 2   | R/W | BCD 3  | of high memory page control.
| 3   | R/W | BCD 4  | of high memory page control.
| 4   | R/W | BCD 16 | of high memory page control.
| 5   | R/W | MD3S0  | BCD 4 of the colour look-up address available only in mode 3.
| 6   | R/W | MD3S1  | BCD 8 of the colour look-up address available only in mode 3.
| 7   | R/W | MCNTRL | If this bit is set when the CPU addresses high memory, then the external signal XMEM goes low and the Coupé looks on its expansion connector for memory sections C and D (addresses 32768 to 65536).

(See section entitled CLUT IN MODE 4 & MODE 3 in the text ahead)

**LMPR** - Low Memory Page Register (250 dec)

This read/write register is used mainly for the control of paging low memory in the CPU's addressing range.

| Bit | R/W |        ||
|-----|-----|--------|-----------------------------
| 0   | R/W | BCD 1  | of low memory page control.
| 1   | R/W | BCD 2  | of low memory page control.
| 2   | R/W | BCD 4  | of low memory page control.
| 3   | R/W | BCD 8  | of low memory page control.
| 4   | R/W | BCD 16 | of low memory bank control.
| 5   | R/W | RAM0   | when bit set high, RAM replaces the first half of the ROM (ie ROM0) in section A of the CPU address map.
| 6   | R/W | ROM1   | when bit set high, the second half of the ROM (ie ROM1) replaces the RAM in section D of the CPU address map
| 7   | R/W | WPRAM  | Write Protection of the RAM in section A of the CPU address map is enabled when this bit is set high.

**MIDI OUT** port (253 dec)

By writing a data byte to this port, the hardware automatically transmits through the MIDI out channel at 31.25 kbaud, the standard for MIDI protocol. Bit 4 of the STATUS register (249 dec) is set high when this register is full.

**BORDER** port (254 dec)

This output port mainly controls the border colour of the screen by supplying a 4-bit address to the Colour Look Up Table (CLUT), to enable a colour to be displayed during border time.

| Bit |       ||
|-----|-------|------------------------------------
| 0   | BCD 1 | of CLUT address for border colour.
| 1   | BCD 2 | of CLUT address for border colour.
| 2   | BCD 4 | of CLUT address for border colour.
| 3   | MIC   | output control bit, normally set high.
| 4   | BEEP  | output control bit, normally set low.
| 5   | BCD 8 | of CLUT address for border colour.
| 6   | THROM | bit set high to allow through MIDI operation
| 7   | SOFF  | bit set high to disable screen display, only active in screen modes 3 and 4, also removes memory contention during off period.

**LINE INT**errupt register (249 Dec)

This write-only register will cause an interrupt to the CPU at the end of the scan-line before the one matching its contents, (ie at the start of the right hand border). This works even for the first scan line. Line numbers are from 0 to 191. This function is always enabled, so to inhibit its operation a false line number from 192 to 255 can be entered. A useful function of this register can be to switch video modes or change colour lookup table values.

**CLUT** - Colour Look Up Table (base port 248 dec)

There are 16 write only 7 bit registers in the CLUT:

| Colour| Register | Port | Hex
|-------|----------|------|-----
|  0    | 0        |  248 | 0F8
|  1    | 1        |  504 | 1F8
|  2    | 2        |  760 | 2F8
|  3    | 3        | 1016 | 3F8
|  4    | 4        | 1272 | 4F8
|  5    | 5        | 1528 | 5F8
|  6    | 6        | 1784 | 6F8
|  7    | 7        | 2040 | 7F8
|  8    | 8        | 2296 | 8F8
|  9    | 9        | 2552 | 9F8
| 10    | A        | 2808 | AF8
| 11    | B        | 3064 | BF8
| 12    | C        | 3320 | CF8
| 13    | D        | 3576 | DF8
| 14    | E        | 3832 | EF8
| 15    | F        | 4088 | FF8

Each register has 7 bits to represent 1 of 128 possible colours.

| Bit |        ||
|-----|--------|--------------------------------
| 0   | BLU0   | least significant bit of blue.
| 1   | RED0   | least significant bit of red.
| 2   | GRN0   | least significant bit of green.
| 3   | BRIGHT | half bit intensity on all colours.
| 4   | BLU1   | most significant bit of blue.
| 5   | RED1   | most significant bit of red.
| 6   | GRN1   | most significant bit of green.

The registers at switch on will be loaded from the ROM with a default set of values corresponding to:

| Register | Colour         | #
|----------|----------------|----
| 0        | black          |   0
| 1        | blue           |  16
| 2        | red            |  32
| 3        | magenta        |  48
| 4        | green          |  64
| 5        | cyan           |  80
| 6        | yellow         |  96
| 7        | white          | 120
| 8        | black          |   0
| 9        | bright blue    |  17
| A        | bright red     |  34
| B        | bright magenta |  51
| C        | bright green   |  68
| D        | bright cyan    |  85
| E        | bright yellow  | 102
| F        | bright white   | 127

The colour numbers are found by:

````
FOR c=0 TO 15 : PRINT PEEK (&55D8+c) : NEXT c
````

A typical routine for loading the CLUT from a memory table:
````
    ld hl,table ; load HL with top of table
    ld b,16     ; load B with size of table
    ld c,248    ; load C with port address

    otdr        ; execute a decrement B, output to port (C) and decrement HL until B=0

    ret         ; return to calling routine
````

CLUT IN MODE 4 & MODE 3

MODE 4

In screen mode 4, 4 bits are used to address the CLUT for the colour of a pixel. Within a byte, the most significant nibble refers to the first pixel and the least significant nibble refers to the second pixel.

MODE 3

The situation is similar in screen mode 3, however this time there are only 2 bits per pixel which address the CLUT. Out of an 8-bit data byte, the first two most significant bits are used as the address for the first pixel.

Normally, only 4 of the sixteen possible registers would be available. This is overcome by using an extra two bits from the high memory page register (HMPR-251 dec). Bit 5 of HMPR is used to access BCD 4 of the colour look up address and bit 6 of HMPR is used to access BCD 8 of the colour look-up address.

In this way, we can still access the 16 colours specified in the colour look-up table whilst having high resolution graphics.

## Read (Input) Ports

**ATTRIBUTES** register (255 dec)

This register enables the programmer to read the attributes of the currently displayed character cell in modes 1 and 2, and the third byte in every four displayed in modes 3 and 4.

**KEYBOARD** register (254 dec)

This read only register is mainly used for inputting the lower 5 bits of the keyboard matrix. It is also the input for the MOUSE when the address lines AD8 - AD15 are high.

| Bit |      ||
|-----|------|----------------------------------------
| 0   | K1   | keyboard matrix line 1, Mouse Control.
| 1   | K2   | keyboard matrix line 2, Mouse Up.
| 2   | K3   | keyboard matrix line 3, Mouse Down/Button 2.
| 3   | K4   | keyboard matrix line 4, Mouse Left/Button 1.
| 4   | K5   | keyboard matrix line 5, Mouse Right/Button 3.
| 5   | SPEN | light pen strobe/serial input bit.
| 6   | EAR  | serial input from EAR of cassette recorder.
| 7   | SOFF | status bit show if external memory is set.

**MIDI IN** register (253 dec)

This read-only register generates an interrupt to the CPU when a data byte has been read from the MIDI serial input interface. The data must be read by the CPU before the next interrupt (typically 320 µS).

**STATUS** register (249 dec)

This read-only register is mainly used for reading interrupt status. Although all five interrupts go to the CPU operating under mode 1 interrupt, there is no way of knowing which one is requesting, therefore a read of this register is necessary. Approximate interrupt times are 20 µs long.

| Bit |            ||
|-----|------------|--------------------------------------------------------------
| 0   | LINE int   | when low, signals the line interrupt register is requesting.
| 1   | MOUSE int  | when low, signals the mouse requests the interrupt.
| 2   | MIDIIN int | when low, signals the MIDI channel has a data byte.
| 3   | FRAME int  | when low, signals the frame scan has been completed (50 per/second).
| 4   | MIDOUT int | when low, indicates the MIDI out register has just completed data output.
| 5   | K6         | keyboard matrix line 6.
| 6   | K7         | keyboard matrix line 7.
| 7   | K8         | keyboard matrix line 8.

**PEN** registers (LPEN - 248 dec) (HPEN - 504 dec)

If the light pen is not connected, these read-only registers are continuously updating with the current position of the scan. The LPEN register is connected to the horizontal or X co-ordinate of the scan function and HPEN is connected to the vertical or Y coordinate of the scan function.

The first two bits of the LPEN register are:

| Bit |        ||
|-----|--------|----------------------------------------------------------
| 0   | BCD 1  | Inputs BCD 1 of the current colour look up table address.
| 1   | TXFMST | is the status bit for MIDI OUT. When this is high it shows that a byte is being transmitted.

# Philips SAA1099 Sound Chip

## Introduction

The sound chip has six tone registers or oscillators and two noise generators. These can all be panned individually from left to right across the stereo field using one of the 256 possible positions, (ie. 16 volumes per channel, thus 16 x 16 combinations gives 256 positions). The position in the stereo field, relating to that particular oscillator, is controlled by its amplitude register. The overall sound can be enabled or disabled using output mixer (28). To hear sound, this register should be '1', to kill the sound, it should be 0.

````
+-------------+
|   Noise     |
| Generator   |--+
|         (22)|  |                              +-----+
+-------------+  |   Enable                     |     |
                 |    Mixer                     |  O  |
+-------------+  |   +----+   +-------------+   |  u  |
|             |  |-->|(21) \  |  Amplitude  |-->|  t  | Left
| Generator 0 |--+   |Bit 0 >-| Generator 0 |   |  p  |------>
|          (8)|  |-->|(20) /  |          (0)|-->|  u  |
+-------------+  |   +----+   +-------------+   |  t  |
                 |                              |     |
+-------------+  |   +----+   +-------------+   |  M  |
|             |  |-->|(21) \  |  Amplitude  |-->|  i  | Right
| Generator 1 |--+   |Bit 1 >-| Generator 1 |   |  x  |------>
|          (9)|  |-->|(20) /  |          (1)|-->|  e  |
+-------------+  |   +----+   +-------------+   |  r  |
                 |                              |     |
                 |                              | (28)|
              To Enable                         +-----+
            Mixer Bit 4
````

The six oscillators are split, three per noise generator. enables the two envelope registers to be used independently.

## Noise & Sound

Mixer registers 20 and 21 mix the noise with each of the oscillators. Register 20 controls whether an oscillator's sound is passed or stopped, whilst register 21 controls the noise.

Example:

````
+-------------+
|   Noise     |
| Generator   |--+
|         (22)|  |                    Noise and/or          +-----+
+-------------+  |       Enable         Tone                |     |
                 |        Mixer         |                   |  O  |
+-------------+  |   +----------------+ | +-------------+   |  u  |
|             |  |-->|(21) Noise      | v |  Amplitude  |-->|  t  | Left
| Generator 0 |--+   |                |-->| Generator 0 |   |  p  |------>
|          (8)|  |-->|(20) Oscillator |   |          (0)|-->|  u  |
+-------------+  |   +----------------+   +-------------+   |  t  |
                 |                                          |     |
                 |                        +-------------+   |  M  |
                 |                        |  Amplitude  |-->|  i  | Right
                 |                        | Generator 1 |   |  x  |------>
                 |                        |          (1)|-->|  e  |
                 |                        +-------------+   |  r  |
                 |                                          |     |
                 |                                          | (28)|
              To Enable                                     +-----+
            Mixer Bit 4
````

Using this mixer allows either noise or tone or both or nothing to be passed to a single amplitude register and so to a precise position in the stereo field.

## Pitch

The pitch of each complete oscillator is controlled by two parameters. These are eight possible octaves per generator and 256 possible tones per octave. By carefully choosing octave and tone register data, a smooth transition is possible from the lowest frequency on this sound of 31Hz to the highest frequency of 7.81KHz.

## Music

Chromatic scales are possible using the table below. Please note also, that the tone numbers are also valid for the other octaves of the same note although tuning may be difficult towards the lower octaves.

## The Chromatic Scale

NB: All numbers given in decimal.

| Note | Tone <br> Number <br> (decimal) | Octave <br> Number | Required <br> Frequency <br> (Hz) | Actual <br> Frequency <br> (Hz)
|----|-----|----|---------|-
| Middle C | 33 | 03 | 261.626 | 261.506
| C# |  60 | 03 | 277.183 | 277.162
| D  |  85 | 03 | 293,665 | 293.427
| D# | 109 | 03 | 311.127 | 310.945
| E  | 132 | 03 | 329.628 | 329.815
| F  | 153 | 03 | 349.228 | 349.162
| F# | 173 | 03 | 369.994 | 369.822
| G  | 192 | 03 | 391.995 | 391.850
| G# | 210 | 03 | 415.305 | 415.282
| A  | 227 | 03 | 440.000 | 440.141
| A# | 243 | 03 | 466.164 | 466.418
| B  |   5 | 04 | 493.883 | 494.071
| C  |  33 | 04 | 523.251 | 523.013

## Octave Registers

Register 16 is an octave register altering the octave of tone registers 8 and 9. This is made possible by only using three bits per tone register to select the required octave.

Thus 2x2x2 gives us eight possible octaves as previously mentioned. So, to access the octave register for tone register 8, we must supply a number (0-7) to the lower 3 bits of register 16. If we needed to access the octave for tone register 9, we would then need to supply a number between 16 and 64 making sure that the first four bits D0-D3 contain zero, or the octave number for tone register 8 if in use.

Example:

Required Octave 5 For Tone Register 8 only

|B7|B6|B5|B4|B3|B2|B1|B0||
|--|--|--|--|--|--|--|--|-
|X |0 |0 |0 |X |1 |0 |1 | X = Don't Care

Number output to Register 16 = 5

Required Octave 6 For Tone Register 9 only

|B7|B6|B5|B4|B3|B2|B1|B0||
|--|--|--|--|--|--|--|--|-
|X |1 |1 |0 |X |0 |0 |0 | X = Don't Care

Number output to Register 16 = 96


## Amplitude Registers

Any data sent to a particular amplitude register can precisely control the position of a sound in the stereo field.

This is made possible by using the same technique as for the octave register. The only differences being that this time 4 bits are used to convey the volume of each channel, and the two 'halves' of the binary number refer to two channels (left and right) instead of two separate tone registers.

Volume 11 required on left channel.
Volume 7 required on right channel for amplitude register 2

|B7|B6|B5|B4|B3|B2|B1|B0
|--|--|--|--|--|--|--|--
|0 |1 |1 |1 |1 |0 |1 |1
|R |R |R |R |L |L |L |L

This would place the sound towards the left side of the stereo field.

## Noise Generators

We have two noise generators again controlled by one register. The operation is very similar to that of the octave registers, but this time only 2 bits are used per noise generator. This gives 4 possible noise clock frequencies. Three of these options are preset - namely:

|  ||
|--|---------
|0 | 31.25KHz
|1 | 15.6KHz
|2 | 7.8KHz

The fourth option (External) is controlled by the frequency of Generator 0 in the case of Noise generator 0 or Generator 3 in the case of Noise Generator 1. Using these generators, we are able to vary the 'pitch' of the noise and/or tone. If only continuously controllable noise is required, the relative tone mixer bit is disabled, but the relative noise mixer bit enabled. This technique is called using a tone generator to "Modulate" the frequency of the noise.

## Envelope Registers

The envelope controllers can be found on registers 24 and 25.

| Bit   |      |
|-------|------|
| 0     | Controls whether the envelope that is set up is mirrored in the left or right channel. (This can be useful to generate a sense of movement without writing to the amplitude registers).
| 1 <br> 2 <br> 3 | Set envelope shape. These three bits select an envelope shape from the table found in Fig 3. in the Philips sound chip data sheet.
| 4     | Controls resolution of envelope if repeated very quickly. 16 levels of resolution controlling envelope modulation are available for repetition up to 977Hz and 8 levels for repetition rates above 977Hz.
| 5     | Controls whether the envelope registers are controlled by generators 1 or 4. If this bit is reset(0), then the internal clock is used to control the shape of the envelope. If this bit is set(1), then the external clock is used(A0) to control the envelope.
| 6     | Not used.
| 7     | Enable or disable the operation of the envelope controller. Note that this bit should be set (1), to enable envelope control.

# The SAM Coupé Software

# Memory

Several memory arrangements are possible with the Coupé, with various advantages and disadvantages, and each of these sections is discussed in detail. The screen mode and the location of screen memory are perhaps the first factor to consider.

## SAM Coupé Memory Map

| Hex  ||
|------|-
| FFFF |
|      | ROM1 or program, variables or screen
| C000 |
|      | Program, variables or screen
| 8000 |

| Hex  |                  ||
|------|------------------|-
|      |Start of channels | CHANS
| 5CB6 |
|      | System variables |
| 5A00 |                  |SVARS
|      | Keyboard table
| 58E0 |                  | KTAB
|      | DEF KEY buffer   | DKLIN
| 5800 |                  | DKBU
|      | Line interrupt colour table
| 5600 |                  | LINICOLS
|      | Palette table
| 55D8 |                  | PALTAB
|      | UDG patterns CHR$(127 - 168)
| 5490 |                  | UDGS
|      | Character patterns CHR$(32 - 127)
| 5190 |                  | CHARS
| 5120
|      | Page allocation of 33 bytes. (1 per 16K page + FFH)
| 5100 |                  | ALLOCT
| 50FF
|      | General-purpose buffer space
| 4F00
|      | Machine stack    | SP
|      | Floating point calculator stack | STKEND
| 4D00 |                  | STKBQT
| 4C00 | FARLDIR buffer
| 4BA0 |                  | HDL
| 4B50 | Tape headers
| 4B00 |                  | HDR
|      | BASIC stack for GOSUB / DO / PROCEDURES | STKBOT<br>BASSTK
|      |                  | BSTKEND
|      | Spare for heap or BASIC stack
|      |                  | HEAPEND
|      | System heap. 2.7K available, doesn't page
| 4000 |                  | HEAPST
|      | ROM0
| 0000 |

## Screen memory location

A complete screen takes 6.75K in mode 1 and 12K in mode 2 (not including a 2K gap between pixel and attribute data). In these modes the memory containing the screen can be switched in at any 16K boundary. The paging system means that the other 16K RAM page in the same half of memory will page at the same time as the page containing the screen. Modes 3 and 4 require 24K and thus two 16K pages. You can either leave the screen memory permanently paged in or just page it in when you want to read it or write to it, providing your screen handling code is paged in at the same time! The ROM switches in the screen as it requires, in sections C and D of the memory map (8000H).

## The Stack

The ROM normally keeps the machine stack and system variables in section B at 4000H-5CD0H, so that they are not paged out when the screen, Basic program or variables area are paged in in the top half of memory.

# ROM

ROM0 is normally switched into section A of the memory map. ROM1 is normally switched out until it is needed; when in use it is located in section D. Jump table routines in ROM0 that need ROM1 will page it in automatically, use it, and then restore its previous status.

## Use Of ROM Subroutines

The ROMs usually expect the stack to be in section B, and many routines require the system variables in the same area to be intact. However, if you wish to use this area for your own code, you can page out the system variables and use the ROM routines indirectly via JSVIN (see later). This routine will switch the system variables back in temporarily while the ROM routine of your choice is executed. The screen will be temporarily switched into section C and D if required, but your code can usually be located in the same area. Naturally, ROM0 must be enabled if you want to use the jump table, but you could page it out most of the time.

For example, you could load your machine code, disable interrupts, switch out ROM0, switch new RAM into section A/B, and use it for your program. You could provide some code to handle maskable and/or non-maskable interrupts, if desired. Before using a ROM routine, enable ROM0 from somewhere outside section A, and use JSVIN to call the routine you want. If you switch the page your code is currently executing in, remember that the next instruction will come from the new page!

## Using Screen Modes 3 And 4

The arrangement of screen memory in modes 3 and 4 makes plotting a pixel very simple. A method similar to that used by the ROM for mode 4 (256*192, 16 colour) is shown below. On entry, L and H are the X and Y coordinates (0,0 at top left) and D has the colour to use in both its nibbles (e.g. D=77H for colour 7). H and L are returned unchanged (convenient, for example, during line drawing).

````
plotlh:
    scf
    rr h
    rr l
    ld a,(hl)
    jr c,PlotOdd   ; jr if odd pixel

    xor d
    and 0FH
    xor d          ; mix left nibble of D with right nibble read from screen
    ld (hl),a
    add hl,hl      ; restore entry HL
    ret

PlotOdd:
    xor d
    and 0F0H
    xor d
    ld (hl),a
    add hl,hl
    inc l          ; restore entry HL
    ret
````

The address of the next scan line can always be obtained by adding 128 to the current screen address.

The screen can be easily moved left or right by 1 pixel using the RLD and RRD instructions provided by the Z80. LDIR and LDDR can be used for 2, 4, 6 etc. pixel moves. The ROM subroutines support most possibilities.

## Palette Switching

The ROM interrupt routine sets up the palette registers (CLUT) at the start of every frame, using one of two tables of 16 bytes at PALTAB, and switching between them to give flashing colours. It is a good idea to keep these tables up-to-date with the current colours, even if you do not want to use the ROM routines, because the palette registers themselves cannot be read. Software entered via MNI would find an accurate PALTAB useful when doing screen dumps or palette alterations.

The ROM can also change a specified palette memory to a given value at a specific scan line, allowing many more than 16 colours to be displayed at once. If only a single change is made per scan line, it will occur during the scan flyback time and no flicker will occur in the display. In the Coupé's striped start-up screen all the stripes are actually palette colour 0 - but palette memory 0 is being altered.

If more than one palette change is programmed to occur at a given scan line, the later changes will occur as the picture is displayed, and this can cause flicker if the colour being altered is on-screen at that particular location. Up to 127 changes can be made per frame. If you wish to provide your own routine this can be added using the line interrupt vector address (LINIV), or by switching out the ROM.

## The Paging System

The paging system makes it possible to page in any address so that there are at least 16K bytes above it before FFFFH is passed. This means that when dealing with data structures less than 16K long, once the start of the data is paged in there is no need to take special precautions to ensure pointers do not "fall off" the end of memory. The ROM normally uses memory sections C and D as a “rotating window" onto memory and keeps system variables and the stack in section B. For example when the next Basic line is pointed to by adding a number to HL (adding current line length to current line start) code similar to that below checks to see if HL has moved out of section C into section D. If so, the page value is increased and HL is adjusted to point to the same actual byte, at an address 4000H lower, in section C. The whole line can then be dealt with fairly simply since no further checks of HL need be made until the next line is looked at.
````
    bit 6,h
    jr z,Lab1

    in a,(HMPAGE)
    inc a
    out (HMPAGE)
    res 6,h

Lab1:
    ETC.
````
Here there is no danger of the lower 5 bits of HMPAGE being incremented past 1FH to corrupt the upper bits, since the last line of program has a terminator. This will be the case with most other data structures you are likely to want to use.

## ROM Resources

The ROM should be used via the documented fixed locations or the jump table to avoid problems with new ROM issues. References are made to ROM 1.0 and ROM 1.2. All production machines contain ROM 1.0, however a free upgrade will allow users to change this to ROM 2.0, which is the production version of ROM 1.2. Production machines will be fitted with ROM 2.0 by mid 1990. The ROM version installed can be determined by: ``PRINT PEEK 15``, and dividing the value displayed by 10.

### Fixed Routines Near The Start Of Lower ROM

| Hex  | |
|------|-
| 0000 | MACHINE INITIALISATION
|      |
| 0004 | ``pop hl`` Call here to return your own address in HL.
| 0005 | ``jp (hl)``

The two instructions above provide the ability to (effectively) use CALL within relocatable code. For example:
````
    call 0004H         ; get address of HERE in HL
here:
    ld de,there-here
    add hl,de          ; add displacement to get address of THERE
    call 0005H         ; effectively, CALL THERE
 etc.

there:
    ret
````
The method above corrupts HL and DE, but it can be adapted to use the alternate register set or IX or lY if desired.

| Hex  | |
|------|-
| 0006 | ``jp (iy)``
| 0008 | ERROR HANDLER
| 000F | ROM VERSION NUMBER
| 0010 | Print char in 'A' register to current stream. The 'K' and 'S' channels respond to control codes for PEN, PAPER, OVER, INVERSE, FLASH, delete, left, right, up, down, AT, TAB and carriage return.
| 0013 | Print BC bytes starting from DE, using current stream.
| 0016 | ``jp (bc)``
| 0018 | Get current character from Basic line.
| 0020 | Get next character front Basic line.
| 0028 | Call floating point calculator. The example multiplies the top two numbers on the floating point calculator stack, then divides the result by 10 and swops top and third no.s.
|      | ``rst 28H ; a,b,c,d``<br>``db MULT ; a,b,c*d``<br>``db STKTEN ; a,b,c*d,10``<br>``db DIVN ; a,b,c*d/10``<br>``db SWOP13 ; c*d/10,b,a``<br>``db EXIT``

The operation codes used are different from the Spectrum's, and more numerous; see the separate section on the floating-point calculator. Note: The vector address RST28V makes it possible to translate any operation code into another before the operation is performed.

| Hex  ||
|------|-
| 002B | ``djnz 002B`` Useful for uncontended timings.
| 002D | ``jp (ix)``
| 0030 | USER RST. Intended for debugging etc. JPs to the address in "RST3OV".
| 0033 | ``jp (de)``
| 0035 | ``djnz 0035H`` Useful for timing.
| 0037 | ``ret``
| 0038 | MODE 1 INTERRUPTS
| 005C | ``out (hmpr),a``
|      | ``jp (hl)``
| 005F | ``ld a,b`` Useful for timing.
|      | ``or c``<br>``dec bc``<br>``jr nz,005F``<br>``ret``
| 0066 | NON-MASKABLE INTERRUPTS

RAM contention means that ROM routines usually run slightly faster than identical RAM routines. If you are executing the Z80's block instructions on large blocks, and speed is important, it might be worthwhile to call the routines below:

| Hex  ||
|------|-
| 008F | ``ldir: ret``
| 0092 | ``lddr: ret`` (block moves run about 8% faster in ROM)
| 0095 | ``cpir: ret``
| 0098 | ``cpdr: ret``
| 009B | ``otir: ret``
| 009E | ``otdr: ret``

JUMP TABLE AT 0100H

Sometimes conditions for entry a few bytes past the start of a routine are given, as well as the usual entry conditions to the routine; where this is done, you can read the routine address from the jump table, add a displacement, and enter part-way through (for example using CALL HLJUMP). The documented entry conditions will remain constant.

When routines are described as "generating an error” this means that error handling (using RST 08H) will clear the machine stack back to the value held in ERRSP and then do a RET. Normally this leads to an error message being given in the lower screen window, but this can be avoided by PUSHing the address of your own error handler onto the stack, and altering ERRSP (possibly temporarily) to hold the current Stack Pointer. When you gain control, ERRNR will hold the error number (see the list in the Basic manual).

| Hex  | Name      | Description
|------|-----------|-------------
| 0100 | JSCRN     | Select screen held in the C register (1-16). Equivalent to Basic's SCREEN command. An error is generated if the screen is not open. This Jump Table entry is not available in version 1.0 of the ROM
| 0103 | JSVIN     | Call parameter word with system variables page switched in. HL', DE', BC' and F are corrupted, and interrupts are enabled, before the parameter address is called. All other registers are passed intact. On exit, all registers except AF' have the values left in them by the called routine. The original status of HMPR is restored. For example:<br><br>``call JSVIN``<br>``dw JGETINT``<br>``ld (STORE),hl etc.``
| 0106 | JHEAPROOM | Reserve BC bytes in the system heap. This is always paged in; it is in the same page as the stack and the system variables, paged into memory area B. On entry, BC=bytes to reserve (if BC is positive) or bytes to release (if BC is negative). On exit, if the carry flag is set the call was successful, and DE points to the old HEAP END (the start of the reserved space), HL points to the new HEAP END (one byte past the end of the reserved memory), and BC is unchanged. If the carry flag is reset, not enough space was available, and HL holds the amount that the request exceeded the available space by.
| 0109 | JWKROOM   | Open BC bytes in workspace (a temporary work area, cleared before each Basic statement is dealt with). On exit, DE points to the reserved space, starting in section C of the memory map, paged in. HL points one byte past the end of the space, provided it is less than 16K long. A and BC are unchanged.
| 010C | JMKRBIG   | Open A 16K pages and BC bytes at HL in section C of the memory map. BC must be 0-3FFFH. This routine can be used to open space before the Basic program, inside it, in the variables area, or the workspace. If there is not sufficient space, an error will be generated. On exit, HL points to the space and DE points to the end of the space (if the space <16K).
| 010F | JCALLBAS  | Call BASIC subroutine at line HL. When RETURN is used, or any error occurs (for example, STOP, variable not found, etc. - even "OK" counts, in this case), your machine code will be re-entered. On return, A holds an error code, or zero if there was no error (and the zero flag will be set if there was no error). When your machine code finally does a RET to return to Basic, the statement that called the code in the first place, such as CALL 54000 or PRINT USR 54000, will be completed, but then the program will carry on at the statement after the RETURN in the Basic subroutine, or after the point where an error occurred, because Basic's notion of its current line and statement have been altered during the subroutine execution.<br><br>To return to the statement after your CALL, or anywhere else in the program for that matter, read the values from SUBPPC and PPC before using any Basic subroutines, then INC the SUBPPC value and place it in NSPPC, and place the old PPC into NEWPPC. This will cause a GO TO of the specified line and statement when your machine code RETs.
| 0112 | JSETSTRM  | Set the stream specified by the A register (FBH-10H).<ul><li> FBH=channel 'B' (Always) Printer binary output.<li>FCH=channel '$' (Always) Output to a string.<li>FDH=channel 'K' (Always) Lower screen I/O.<li>FEH=channel 'S' (Always) Upper screen I/O.<li>FFE=channel 'R' (Always) Output to edit line.<br><br><li>00H=channel 'K' (Usually)<li>01H=channel 'K' (Usually)<li>02H=channel 'S' (Usually)<li>03H=channel 'P' (Usually) Printer text output.</ul>
| 0115 | JPOMSG    | Output message number A from table at DE. Zero gives the first message. Each message should have bit 7 set on the last character. Characters 0-31 should not be included. The current output stream is used.
| 0118 | JEXPT1NUM | Syntax check/evaluate a numeric expression. During syntax checking an invisible 5-byte form of any literal numbers is inserted. During run time the result of the expression is left on the floating point calculator stack.
| 0116 | JEXPTSTR  | Syntax check/evaluate a string expression. See JEXPT1NUM.
| 011E | JEXPTEXPR | Syntax check/evaluate an expression. See JEXPT1NUM. These three routines can be useful in extending the Basic interpreter.
| 0121 | JGETINT   | Unstack number from calculator stack into HL. BC holds a copy of HL, and A holds a copy of L. An error is generated if the rounded number is not in the range 0- 65535.
| 0124 | JSTKFETCH | Unstack last value from calculator stack to AEDCB. If the value is a floating-point number, the 5 bytes are in CPC/Spectrum format. If the value is a whole number between 0 and 65535 (which may be negative) it may be in a special form where A=O (showing special form), E=SGN (0=positive, FFH=negative) and D and C are less and more significant bytes. If the value is a string, A holds the page the string text starts in, DE holds the start address of the text start within the page (8000-BFFF), and BC holds the string length.
| 0127 | JSTKSTORE | Stack AEDCB registers on the calculator stack. On exit, HL holds the new STKEND, and AEDCB are unchanged. No other registers are altered.
| 012A | JSBUFFET  | Unstack the details of a string from the calculator stack and copy the text to a buffer in the system page in section B of the memory map. Paging is undisturbed on exit, no matter where the string is copied from. Generates an error if the string is more than 255 characters long, or the null string. On exit, DE points to the start of the buffer and BC holds the string length. The A register holds a copy of C.
| 012D | JFARLDIR  | Copies bytes from page A, offset HL to page C, offset DE. Copies (PAGCOUNT) 16K pages and (MODCOUNT) bytes (MODCOUNT=0000-3FFF), paging as needed. The paging state on entry is unimportant, and is unchanged on exit. Since the routine copies via a buffer, it is usually possible to write a faster, more specialised routine if the required paging can be arranged.
| 0130 | JFARLDDR  | A LDDR version of FARLDIR.
| 0133 | JPUT      | Screen modes 3 and 4 only. Place a block of data on the screen at given coordinates. <br><br> On entry, C holds the x coordinate (bit 0 is not significant, since the data can only be aligned to byte accuracy). The x-range is 0-255, whatever the MODE. <br><br> The B register holds the y coordinate, with 0 at the top of the screen and 191 at the bottom. <br><br> The HL register points to the data to use; the first and second bytes of the data specify width in bytes and height in pixels, followed by 811 bytes for the top scan of the block, all bytes of the second scan, etc. <br><br> The A register determines the method of placing the data on the screen. 0=overwrite with INVERSE option, 1=XOR, 2=OR, 3=AND, 4=overwrite (with no INVERSE option - faster), 5=mask. The mask option requires a second block of data the same length as the first (excluding the first 2 bytes of the first block) pointed to by HL', with bits set for "unmasked" and reset for "masked". This allows a complex shape, perhaps with holes in it, to be placed on a background without border effects. If the shape hangs off the bottom of the screen, it will be "trimmed' to fit. If the data overlaps the right border of the screen, it will wrap round to the left, but 1 scan lower. <br><br> Both HL and HL' (if used) must point to data that will be available for use; since JPUT will temporarily switch in the current screen (using CUSCRNP, or at least the contents of that address) at 8000H, the data must be located at 4000-7FFFH, or EOOO-FFFFH in the screen page. JPUT also needs to use the system variable CURP (or a byte at that address) as a temporary store, and it will read INVERT to determine INVERSE status, where this is an option. JPUT should run rather faster than Basic's PUT, since Basic has to move data from the variables area. <br><br> Unlike attribute colour systems, the colours to be used are implicit in the block data, although methods 0-3 allow an INVERSE option. The restriction that blocks must be put down at even pixel boundaries is to keep the speed high. If you wish to place blocks at 1-pixel intervals, it is possible to prepare two versions of the same graphic, with the data displaced by 1 pixel in one of them, in order to get the required effect. <br><br> In version 1.0 ROMs there is an error in JPUT, but you can get the same effect by using: ``PUSH AF: CALL 3A7BH: POP AF: CALL 2DACH`` instead of ``CALL 0133H``. If the ROM version number (PEEK 15) is not 10, you must use 0133H.
| 0136 | JGRAB     | Screen modes 3 and 4 only. Store a block of screen data from given coordinates to a buffer. <br><br> On entry, C holds the x coordinate (bit 0 is not significant) and the x-range is 0-255 whatever the screen MODE. B holds the y coordinate, with 0 at the top of the screen and 191 at the bottom. E holds the block width in bytes, and D holds the length in pixels. On exit, DE points to the start of the block in the current screen page (specified by CUSCRNP); the first byte is always zero, the next byte is the width in bytes, the next byte is the length in pixels, and the following bytes store the block, scan line after scan line. BC holds the block length, including the a header bytes. Since the area is stored in the "spare" 8K following a MODE 3/4 screen, the length of the data must be a little under 8K, at the most. JGRAB requires temporary storage at the variable CURP (or storage at that address) and it will read CUSCRNP in order to temporarily switch the screen in. If the GRABed area hangs off the bottom of the screen, it will be trimmed as needed.
| 0139 | JPLOT     | Plot pixel at x coordinate in C and y coordinate in B, except when the MODE is 3 and FATPIX 0 is in force (THFATT will be zero); in which case use HL as the x coordinate (0-511) and plot a "thin" pixel. The y-axis has 0 at the top and 191 at the bottom in all cases. There is no control to prevent you plotting beyond the bottom of the screen.
| 013C | JDRAW     | Draw a line from the current position C (or HL if "thin" pixels are in Use, according to THFATT) pixels horizontally and B pixels vertically. D=1 for down (or for no y movement) and FF for up, E=1 for right (or for no x movement) and FF for left. The colour and OVER and INVERSE state come from the temporary graphics variables. The screen used comes from CUSCRNP. An error is generated if the line is drawn over the screen edge.
| 013F | JDRAWTO   | Draw a line from current position to point C,B (or point HL, B if "thin" pixels are in use). The y axis has zero at the top and 191 at the bottom. Colours etc. come from the temporary graphics variables.
| 0142 | JCIRCLE   | Draw circle at C,B radius A. If "thin" pixels are set, HL should hold an offset from the left-hand screen border (in pixels). This allows a circle to be placed anywhere on a mode 3 screen even though the x coordinate is limited to 1 byte. The y axis has zero at the top. Colours etc. come from the temporary graphics variables.
| 0145 | JFILL     | Modes 3 and 4 only. Uses the 16*16 pixel pattern at DE to fill an area starting at coordinates C,B. The y axis has zero at the top. If DE holds zero, a "solid" fill with the current PEN (from M23INKT) is performed. Otherwise DE can have any value (but values 0001-3FFFH will use the ROM as a pattern!). If A=0 then a preliminary transfer of the screen memory to a scratchpad area (6K long, immediately after the 24K screen memory) is made; you will need to make A=0 for at least the first fill you use. Later fills on the same screen over the same colour can make A non-zero for greater speed. <br><br> If you are using MODE 3 with "thin" pixels, HL should hold a byte offset from the left-hand screen edge for the point to start filling at. This allows any part of the screen to be filled, despite the x coordinate being limited to one byte. <br><br> The pattern data pointed to by DE has 8 bytes for the top row, 8 bytes for the next, etc. so 128 bytes are needed. Each nibble controls colour for 1 pixel in mode 4 or 2 pixels in mode 3.
| 0148 | JBLITZ    | Execute a string of graphic commands BC long at DE. DE can be anything from 4000H to FFFFH, and BC anything from 0 to FFFFH (JBLITZ will page if  equired). PLOT, DRAW, DRAW TO, CIRCLE, OVER, INK, CLS and PAUSE commands can be included in the string. They are handled at a higher level than JPLOT, JDRAW and JCIRCLE; the floating point calculator and special Basic variables can be used for offset and scaling. The use of numerous system variables makes having the system variables paged in hard to avoid. x coordinates and moves of 0-255 only are allowed; i.e. only half the screen is easily usable in MODE 3 with FATPIX 0 selected. The coordinate system used is the same as that used by Basic; e.g. bytes 01 00 00 would act like PLOT 0,0 in Basic and be modified if XOS or YOS were altered. To perform a RELATIVE DRAW: <br><br> 00 or FF give the SGN of an x movement (00=positive,FF=negative), followed by the x movement, followed by the SGN of the y movement and the y movement. If movements are negative, they are stored as 256-move. <br><br> ``PLOT``: 01 followed by x,y <br> ``DRAW TO``: 02 followed by x,y <br> ``CIRCLE``: 03 followed by x,y,r <br> ``OVER``: 04 followed by 0-3 <br> ``PEN``: 05 followed by 0-17 <br> ``CLS``: 06 followed by 0-1 <br> ``PAUSE``: 07 followed by 0-255 <br><br> The easiest way to prepare the data for JBLITZ is to use RECORD in Basic and then POKE the string where you need it.
| 014BH | JROLL    | Modes 3 and 4 only. Move part of screen left, right, up or down. The screen area must be an even number of pixels across. A horizontal move by 1 pixel or any even number of pixels is possible. A vertical move by any number of pixels is possible. Wrap-round is optional; it uses the area immediately after screen memory as a buffer. On entry, A is 00 if a SCROLL (no wrap) is wanted, or FFH for a ROLL (with wrap). B holds the pixels to move by, C is a direction code (l=left, 2=up, 3=right, 4=down), D holds length of block in pixels and E holds width of block in pixels (bit 0 is nonsignificant). HL holds the coordinates of the top left-hand corner of the block to be moved, L holding the x coordinate (range 0-255, whatever the MODE) and H holding the y coordinate with 0 at the top of the screen. JROLL checks the MODE system variable, copies the permanent graphics variables onto the temporary ones, and uses M23PAPT as the background colour for new screen generated by SCROLL. The routine uses CURP and TEMPPB3 in the system variables, and up to 0181H bytes at 4D00H to store "unrolled" code loops.
| 014E | JCLSBL    | Clear entire screen if A=0, else clear upper screen.
| 0151 | JCLSLOWER | Clear lower screen. Also selects channel K (lower window input/output).
| 0154 | JPALET    | If A=FFH, put colours BC in PALTAB as main and flashing colours for palette colour E. (Make B=C for no flashing). Colours should be 0-127, palette entry 0-15. If A is nonzero, it is a y-coordinate to alter the palette at. PALTAB is not altered; instead an entry is made in the line interrupt colour table.
| 0157 | JOPSCR    | OPEN SCREEN number C in mode B. The pages required are located in the Page Allocation Table and reserved, and an entry is made in SCLIST. The screen number must be 2-16, and it must not be already open, or an error is generated.
| 015A | JMODE     | Set screen MODE that is in the A register (0-3 gives MODEs 1-4).
| 015D | JTDUMP    | Do a text screen dump (if dump utility installed).
| 0160 | JGDUMP    | Do a graphic screen dump (if dump utility installed). The system variables documented in the Basic manual control the area dumped and its magnification.
| 0163 | JRECLAIM  | Reclaim (close up) BC bytes at HL (8000H-BFFFH). Can be used to close up memory before a Basic program, within it, or in the variables area or workspace. BC must be less than 16K; if you want to reclaim a bigger space, call one byte from the start of the routine, with A holding number of 16K pages to reclaim, in addition to the space specified in BC.
| 0166 | JKBFLUSH  | Flush keyboard buffer.
| 0169 | JREADKEY  | Read keyboard, flush butter (like INKEYS). Z/NC if no key pressed, else NZ/CY and A=key value (ASCII).
| 016C | JWAITKEY  | Read next key into A from keyboard buffer. Wait for a key to be pressed if needed.
| 016F | JBEEP     | Make a beep DE-1 cycles long at period HL*8 T states.
| 0172 | JSAVE     | Save a block CDE bytes long starting at HL (switched into section C). C holds the number of 16K pages, and DE holds the length MOD 16K. Make A register first byte saved, (FFH for 'data block', 01 for SAM 'header', 00 for spectrum header). If SLDEVT (see system variables) holds "T", the SAVE will be to tape-if it holds "N" the SAVE will be to the Network. SLNUMT controls the save speed to tape (112 is standard speed).
| 0175 | JLOAD     | If the carry flag is set, LOAD CDE bytes to HL (switched into section C of the memory map). If the carry flag is reset, do a VERIFY. The A register holds the type of data to deal with (FFH=data block, 01=SAM or Spectrum header, 00=Spectrum header). If SLDEVT holds "T", tape will be used; if "N", the Network. Varying input tape speeds are handled automatically. The routine returns with carry set if the operation was successful; otherwise there has been an error.
| 0178 | JLDVD     | If the carry flag is set, LOAD CDE bytes of data (not header) to HL. If the carry flag is reset, do a VERIFY. Use disk, tape or Net according to the contents of SLDEVT. An error is generated if the operation fails.
| 017B | JEDGE2    | Waits for 2 signal transitions on EAR, returninq in A and C the number of 47-T state units taken. On entry, B should hold the current EAR status in bit 6, bit 3 should be set, and the other bits should reflect what you want sent to the BORDER port when there is a signal transition. Bits 2-0 will be reversed on every transition. The D' register should hold a value that determines the length of a pause between finding one transition and looking for another (this avoids double counts when the tape signal has buzzy edges). For standard speed tapes, D' should be about 46H, JLOAD sets D' according to tape speed. Interrupts should be disabled for accurate results. <br><br> The routine returns Z if it had to wait too long (256 units), NC if ESC was pressed, and CY if okay. Entry 2 bytes from the start avoids the initial zeroing of the C register which is used as a counter; entry 6 bytes from the start waits for only 1 signal transition on EAR. On exit the B register holds a new value suitable for another call to the routine, and A and C both hold the counter value. Note: In version 1.0 ROMs this jump table entry incorrectly has bit 15 of the address set. You should read the address at O17CH, reset bit 15, and CALL that address.
| 017E | JSTR$     | Create ASCII version of number on floating-point calculator stack in buffer at 5BA0H. On exit, DE holds 5BA0H and BC holds the number of characters in the buffer.
| 0181 | JSENDA    | Send the byte in the A register to the parallel printer. The system variable at 5A10H is read to obtain the port to use, and the routine loops until the printer is ready before sending the byte and then returning. If ESC is pressed, an error will be generated. Uses A and BC only.

JUMP TABLE ENTRIES INTRODUCED AFTER ROM 1.0

|      |         ||
|------|---------|-----------
| 0184 | JNCHAR  | Call SCREEN$ subroutine. Try to match the character at line D, column E on the screen with any character in the main character set (pointed to by CHARS) or any character in the set pointed to by UDG. On exit, the carry flag is set if the search was successful, in which case A holds a character code of 20H-7FH (32-127) if the character was found in the main set, or 80H-7FH (128-168) if the character was found in UDG set. If the carry flag was reset, A=0 and the search failed.
| 0187 | JGRCOMP | Subroutine used by graphic dump utility.
| 018A | JGTTOK  | Try to match potential spelled-out keyword pointed to by DE in a list of keywords at HL+1. The list should be in upper case, with bit 7 set on the last letter of each keyword. The A register should hold the number of words in the list, plus 1. On exit no match was found if the zero flag is set. If a the zero flag is reset, the A register holds the entry number in the list (1 or more), HL points to the start of the original word and DE points just past the end of it.
| 018D | JCLSCR  | Close screen number held in the C register.

## Character Set

The character set from CHR$ 32 to CHR$ 130 is stored in compressed form in ROM1 and loaded into RAM in the system variables page when the machine is turned on. CHR$ 131-168 are initially defined as blanks, although CHR$ 128-143 are displayed as block graphics unless "BLOCKS 0" has been set. (The block graphic shapes are generated as needed - the character set itself does not contain them). Characters apart from block graphics occupy a 6*8 matrix, making then suitable for display at 6-pixel or 8-pixel intervals.

Character definitions occupy 8 bytes, from top row of pixels to bottom row. The left and right columns of pixels of this 8*8 block are not used when printing is at 6-pixel intervals. The character set base address is 5190H, and space is available for CHR$ 32 to 168 in one continuous block. An additional system variable, HUDG, can be set up to point to definitions for CHR$ 169-254, but standard designs for characters 128 to 168 are supplied (file 'font') which includes a full set of foreign characters which match the accented characters on most printers. Their use is recommended so that software can easily be converted for use abroad.

## Vectors

These allow important ROM routines to be intercepted by the user. They contain addresses which will be called if (and only if) the most significant byte is non-zero. This gives the option of RETurning (perhaps you decide not to handle a particular case), or discarding the
return address and turning the vector into effectively a JUMP.

Several programmers might want to use the same vector. If your programs simply overwrite vectors they are likely to be incompatible with future utilities from MGT and other software suppliers. We recommend that your programs save the old vector value. Unfortunately, an automatic linking mechanism that made this very easy had to be omitted front the ROM, but the solution is still fairly simple: for example, to add code to provide some action for the STEP token:
````
;Initialise CMDV but store any existing entry first.
init:
    ld hl,(CMDV)
    ld (store),HL
    ld hl,myPatch
    ld (CMDV),hl
    ret

myPatch:
    cp STEPTOKEN
    jr z,myP2       ; JR if we are interested

    ld hl,(store)
    inc h
    dec h
    ret z           ; RET if no address was in CMDV at INIT
    jp (hl)         ; let another routine have a go

myP2:
    (Code to provide some action for STEP)
    ret
````
NB All examples are program fragments, not complete programs, and do not, for example, include the above code, which should be included in actual applications.

### List Of Vectors

| Hex  | Name   | Description
|------|--------|-------------
| 5ADA | DMPV   | Called if the DUMP keyword is used in run-time. CHAD points to 0DH or 3AH if just DUMP was used; otherwise DUMP CHR$ was used.
| 5ADC | SETIYV | SETTY is called when DRAW, PLOT and CIRCLE "decide" what pixel setting routine to use, and itself calls SETIYV if its most significant byte is non-zero. SETIY points the IY register to a suitable routine, and the provision of a vector is intended to allow extra plotting modes, such as dotted lines, to be implemented without all the graphics commands being rewritten. On entry to SETIYV, A holds the current screen mode-1.<br><br> On return to PLOT, DRAW and CIRCLE the IY register should point to a pixel setting routine, and only A and HL should be altered otherwise. In mode 4, and mode 3 when "fat" pixels are selected, the value of A on exit is passed to D' by the graphics commands, and can be used to hold the PEN colour if desired. <br><br> If you alter SETIYV, as with all the vectors, your routine making just RET will cause the normal ROM routine to be executed. Thus your code might start with a check of the mode to see if it is one you want the ROM to deal with, and RET if so. Otherwise, POP the return address so that the ROM routine is never used, and set IY yourself. The next RET will be to DRAW, PLOT or CIRCLE. <br><br> The pixel setting routine that you supply the address of in IY should plot the pixel at L,H and return with only AF changed. The coordinate system used has 0,0 at the top lefthand comer of the screen. You may want to take note of the current OVER, INVERSE and PEN settings. (In which case you may find it speeds things up if, like the ROM, you set IY to a different routine for some options). The routine should end in JP (IX), not RET.
| 5ADE | PRTOKV | Print a token. A=token code to expand and print as ASCII.
| 5AE0 | NMIV   | Non-maskable interrupt. Normally holds the address of a routine that returns to Basic when the BREAK button is pressed. NMIV switches in the system page temporarily, and provides its own stack there, whatever the paging state when the interrupt was generated. On entry, the LMPR status when the NNI occurred is stored in NMILRP, the Stack Pointer when NMI occurred is stored in NMISP, and the AF and HL registers have already been PUSHed onto the stack in use when NMI occurred (which may be paged out).
| 5AE2 | FRAMIV | Called by the frame interrupt 50 times a second. All main registers can be used.
| 5AE4 | LINIV  | Called by the line interrupt, which is generated when the value in the line interrupt register matches the scan about to occur. This vector can be used to alter the palette, change screen or screen mode, etc. in mid-screen. To synchronise such changes with the scan flyback, it is possible to wait for a change at the HPEN port to show that the scan number has just changed. (This will fail if a lightpen is connected, however). All main registers can be used.
| 5AE6 | COMSV  | Called by COMMS interrupt.
| 5AE8 | MIPV   | Called by MIDI input interrupt. On entry, the A register has just been read from the MIDI IN port.
| 5AEA | MOPV   | Called by MIDI output interrupt.
| 5AEC | EDITV  | Called before the editor is used for editing a line or INPUT.
| 5AEE | RST08V | Called early in error handling, with A=error code. The alternate registers have been selected, CHAD and CHADP have been copied to XPTR and XPTRP, DE points to the error code that follows RST 08H, and an address 1 byte past that code is on the stack, underneath the return address to the error handling routine. No clearing of stacks has been done at this stage.
| 5AF0 | RST28V | Called by floating point calculator with A=next code in the list that follows a RST 28H instruction. DE points to the end of the floating point calculator stack. On exit, the IX register should be unchanged, and DE should point to the end of the floating point calculator stack. (This may be different from the entry value, if items have been added, discarded or combined). See example below.
| 5AF2 | RST30V | User RST. Jumped to (Not called like the other vectors) by RST 30H. (ROM0 uses RST 30H to provide a "CALL ROM1" facility, but this only applies to RST instructions used inside ROM0). All registers are passed intact.
| 5AF4 | CMDV   | Called with the A register holding the code of the character about to be syntax checked or executed (normally a command code). Can be used to add commands, or modify the action of the existing ones.
| 5AF6 | EVALUV | Expression evaluator. Called with A=current character in expression; can be used to add new functions.
| 5AF8 | LPRTV  | Called as each character code above 127 is handled by the printer driver, when channel "P" is being used.(More complete control can be obtained by altering the "P" or "B" channel output address - see below). <br><br> On entry to the routine the character code is in the register. For example to transform CHR$ 130 to "A": <br><br>``INIT: ld hl,PATCH`` <br> ``ld (5AF8H),hl`` <br> ``ret`` <br><br> ``PATCH: cp 130`` <br> ``ret nz`` <br><br> ``pop bc ;JUNK RETURN ADDRESS`` <br> ``ld a,65`` <br> ``rst 10H ;PRINT CHARACTER`` <br> ``ld hl,5A70H ;PRINTER COLUMN VARIABLE (SVAR &70)`` <br> ``inc (hl) ;1 COLUMN RIGHT`` <br> ``ret`` <br><br> Instead of using RST 10H to print the new character(s), you might prefer to use either CALL 0181H (send A to parallel printer) or probably better, call the following code to send the A register to channel "B": <br><br> ``CHBOP: ld hl,(5C4FH) ;CHANNELS BASE ADDRESS`` <br> ``ld de,25 ;(use 15 to point to "p" channel)`` <br> ``add hl,de`` <br> ``ld e,(hl)`` <br> ``inc hl`` <br> ``ld d,(hl) ;DE=channel B output address`` <br> ``ex de,hl`` <br> ``jp (hl)`` <br><br> Channel "B" handles all output without fiddling with it; channel "P" responds to control codes, adds auto-LF etc. and then sends its output to channel "B". something like ESC ;"R"; CHR$ 0 should be sent via the "B" channel. Channel "B" normally outputs using 0181H, but if you use CHBOP rather than O181H directly, it will be easier for others to divert printer output to another device, such as a serial interface. (By altering the output address in the channel).
| 5AFA | MTOKV  | Called if a potential spelled-out keyword is not recognised by the ROM. On entry, DE points to the potential keyword. On exit, conditions should match those of jump table entry JGTTOK.
| 5AFC | MOUSV  | Called every frame. when this vector is used, the ROM's own scan of the mouse is bypassed.
| 5AFE | KURV   | Called before the editing cursor is printed (by calling the address in MNOP). ROM1 is on. Could be used to supply a "transparent" or other cursor.

Additional example: Suppose you have a lot of machine code graphics subroutines which require the screen to be switched in at 4000H. It would be nice to modify USR so that any use of the subroutines switched in the required page temporarily; the routine below does this, for machine code located in the top half of memory. INIT is called to alter the floating point calculator ~ vector to point to USRPTCH; whenever the calculator handles a USR, we intercept it, juggle the pages to put the screen at 4000H (taking care with the stack) and call the USR address, stacking BC back on the floating point calculator stack as the result of USR, and returning DE pointing to STKEND and IX unchanged. (All as expected by the calculator).

USRPTCH must be in the system page to guarantee it is resident when the vector is called; the best place is in the system Heap. PART2 must be in the top half of memory, but in any case it is a goad idea to use a short routine in the Heap to call a large routine in another page, since this keeps the Heap train being filled up.

````
init:
    ld hl,USRPTCH
    ld (RST28V),HL
    ret

UsrPtch:
    cp 45H          ; USR code
    ret nz          ; keep things simple and ignore anyone else who might want to use this vector
    pop bc          ; junk RET address
    in a,(HMPR)
    push af         ; save current HMPR status
    ld a,1          ; OK if Part2 in page 1 or 2
    out (HMPR),A    ; page in Part2
    in a,(LMPR)
    and 0BFH
    out (LMPR),a    ; ROM1 off
    call Part2
    in a,(LMPR)
    or 40H
    out (LMPR),a    ; ROM1 on again for RET to calculator
    pop af
    out (HMPR),a    ; original HMPR status restored
    ret

Part2:
    ld (Store),sp   ; we will be switching out the stack so save current SP
    ld sp,TSTACK    ; put a new stack elsewhere (>=8000H)
    push af         ; LMPR status
    push ix         ; calculator needs IX unchanged
    call JGETINT    ; get USR address in BC
    in a,(VPAGE)
    and 1FH         ; A=screen page
    dec a
    out (LMPR),a    ; page it in at 4000H
    call BCJUMP     ; CALL USR address
    pop ix
    pop af
    out (LMPR),a    ; original LNPR status
    ld sp,(Store)   ; original SP
    xor a
    ld e,a
    ld d,c
    ld c,b
    call JSTKSTORE
    ex de,hl
    ret

Store:
    dw 0
````

# Floating Point Calculator Command Codes

The floating-point calculator performs all the mathematical operations of the Coupé, and many of the string operations. Since it provides a simple way of programming quite complex tasks in a sort of sub-language, it can be very convenient. The calculator is called using RST 28H, followed by a series of command codes (which may have parameters). A special code terminates the list. The data that the calculator manipulates is placed on a special stack that we will refer to as the FPCS. All items are five bytes long. The jump table allows registers to be passed to and from this stack, and the B register is passed into and
out of the calculator (see below).

Numbers are held in two forms; the integer form stores whole numbers between -65535 and +65535 as zero, SGN (0 for positive, FFH for negative), less significant and more significant bytes, and a final zero byte. E.g. 80H is stored as 00 00 80 00 00, 4001H as 00 00 01 40 00, -1 as 00 EFF FF FF 00 and -80H as 00 FF 80 FF 00. (Negative values are stored in negated form (65536 minus the number).)

If numbers are in integer form the calculator is often able to use specialised, faster forms of operations such as multiply, subtraction and addition. Numbers outside the -65535 to +65535 have to be held in a different form, as 2 to the power of a number called the exponent, multiplied by another number called a mantissa. The first byte is the exponent +80H, and the other four bytes are the mantissa. This is always between 0.5 and just less than 1, which means that the first bit is always 1, allowing it to be actually used as a SGN bit (0 for positive, 1 for negative).

This scheme allows values between about 1E38 and 1.7E-39 to be stored to an accuracy of 9 or 10 digits. It is important to note that some fractional numbers (such as 1/10) cannot be stored exactly in this binary form (just as, for example 1/3 cannot be represented exactly in
decimal form). This means that if you subtract 0.1 from 1 ten times, the result is not exactly zero. This is not a fault - just a limitation of number systems in general, which you should be aware of.

Strings are held as 16K page of string text start, offset of string text start (8000H-BFFFH, LSB/MSB) and string length (LSB/MSB).

In the list below, the action of many of the calculator codes is shown symbolically. Where a command code deals with two numbers (e.g. multiply) the last number on the FPCS is referred to as N2 and the number below that is referred to as N1. If the values dealt with are strings, $2 and $1 are used.

| Hex |        ||
|-----|--------|-
| 00  | MULT   | N1*N2
| 01  | ADDN   | N1+N2
| 02  | CONCAT | $1+$2 Prepare the concatenated text of $1+$2 in the Workspace, and stack the details of this temporary string.
| 03  | SUBN   | N1-N2
| 04  | POWER  | N1^N2
| 05  | DIVN   | N1/N2
| 06  | SWOP   | Swap V1,V2
| 07  | DROP   | Discard last value
| 08  | MOD    | N1 MOD N2
| 09  | IDIV   | N1 DIV N2
| 0A  | BOR    | N1 BOR N2
| 0B  | Reserved
| 0C  | BAND   | N1 BAND N2
| 0D  | NUOR   | N1 OR N2
| 0E  | NUAND  | N1 AND N2
| 0F  | NOTE   | N1<>N2 Comparisons like <> delete the two compared values from the FPCS and replace them with 1 or 0 (true or false).
| 10  | NLESE  | N1<=N2
| 11  | NGRTE  | N1>=x2
| 12  | NLESS  | N1<N2
| 13  | NEQUAL | N1=N2
| 14  | NGRTR  | N1>N2
| 15  | SAND   | $1 AND N2
| 16  | SNOTE  | $1<>$2
| 17  | SLESE  | $1<=$2
| 18  | SGRTE  | $1>=$2
| 19  | SLESS  | $1<$2
| 1A  | SEQUAL | $1=$2
| 1B  | SGRTR  | $1>$2
| 1C  | SWOP13 | Swop last value and value 2 below.
| 1D  | SWOP23 | Swop second-to-last value and value below it.

The three command codes below, along with DECB, use a displacement byte to skip backwards or forwards in the list of commands (like GO TO in Basic, or JP in assembly language). The isplacement is the distance between the displacement byte and where you want to jump to; if it is greater than 7FH it treated as a backwards jump, for example, FFH is backwards by 1.

| Hex |         ||
|-----|---------|-
| 1E  | JPTRUE  | Jump by displacement given in next byte, if the last value is one. (The last value is discarded).
| 1F  | JFFALSE | Jump by displacement given in next byte, if the last value is zero. (The last value is discarded).
| 20  | JUMP    | Jump by displacement given in next byte.

The calculator has a special store called BREG that initially holds whatever the Z80's B register did when the calculator was called. The four command codes below use BREG.

| Hex |         ||
|-----|---------|-
| 21  | LDBREG  | Load BREG with next byte.
| 22  | DECB    | Decrement BREG and jump by the displacement given in the next byte if BREG is non-zero.
| 23  | STKBREG | Put BREG on FPCS as a number between 0 and 255.
| 24  | USEB    | Take the next calculator code from BREG.
| 25  | DUP     | Duplicate top FPCS entry.
| 26  | ONELIT  | Stack next byte on FPCS (as a number between 0 and 255).
| 27  | FIVELIT | Stack next 5 bytes on FPCS (as any number).
| 28  | SOMELIT | Stack number of bytes specified by next byte, using (next byte+1) as the first byte. (This allows many 5-byte values to be stacked at once).
| 29  | LKADDRB | Use the next 2 bytes as an address; stack the byte found at that address on the FPCS.
| 2A  | LKADDRW | Use the next 2 bytes as an address; stack the word (2 bytes) found at that address on the FPCS.
| 2B  | REDARG  | Fiddle with the argument of SIN.
| 2C  | LESS0   | Stack 1 (TRUE) or 0 (FALSE) according to whether the last value is <0. The last value is discarded.
| 2D  | LESE0   | Stack 1 or 0 according to whether the last value is <=0. The last value is discarded.
| 2E  | GRTR0   | stack 1 or 0 according to whether the last value is >0. The last value is discarded.
| 2F  | GRTE0   | Stack 1 or 0 according to whether the last value is >=0. The last value is discarded.
| 30  | TRUNC   | Chop off the digits after the decimal point in the last value.
| 31  | RESTACK | Transform the last value to full 5-byte form if it isn't already in that form.
| 32  | POWR2   | Calculate 2 to the power of the last value.
| 33  | EXIT    | Finish using floating point calculator.
| 34  | EXIT2   | Finish using floating point calculator, and do a RET.
| 35  | Reserved
| 36  | Reserved
| 37  | Reserved
| 38  | Reserved

The command codes below are used to provide most of Basic's functions:

| Hex |     |
|-----|-----
| 39  | SIN
| 3A  | COS
| 3B  | TAN
| 3C  | ASN
| 3D  | ACS
| 3E  | ATN
| 3F  | LOGN
| 40  | EXP
| 41  | ABS
| 42  | SQN
| 43  | SOR
| 44  | INT
| 45  | USR
| 46  | IN
| 47  | PEEK
| 48  | DPEEK
| 49  | DVAR
| 4A  | SVAR
| 4B  | BUTTON
| 4C  | EOF
| 4D  | PTR
| 4E  | Reserved
| 4F  | UDG
| 50  | NUMBER
| 51  | LEN
| 52  | CODE
| 53  | VAL$
| 54  | VAL
| 55  | TRUNC$
| 56  | CHR$
| 57  | STR$
| 58  | BIN$
| 59  | HEX$
| 5A  | USR$
| 5B  | INKEY$ #
| 5C  | NOT
| 5D  | NEGATE

The calculator has six 5-byte memories for holding temporary results. The following codes store and recall the memories:

| Hex |       ||
|-----|-------|-
| C8  | STOD0 | Copy the last value to calculator memory 0-5, then delete it from the FPCS.
| C9  | STOD1
| CA  | STOD2
| CB  | STOD3
| CC  | STOD4
| CD  | STOD5
|     |
| D0  | STO0 | As above, but do not delete the last value after copying it.
| D1  | STOl
| D2  | STO2
| D3  | STO3
| D4  | STO4
| D5  | STO5
|     |
| D8  | RCL0 | Stack the value in calculator memory 0-5 on the FPCS
| D9  | RCLl
| DA  | RCL2
| DB  | RCL3
| DC  | RCL4
| DD  | RCL5

The codes below provide a compact method of stacking comanonly used constants on the FPCS:

| Hex |           ||
|-----|-----------|-----------
| E0  | STKHALF   | Stack 0.5
| E1  | STKZERO   | Stack zero
| E2  | STX16K    | Stack 16384
| E6  | STKFONE   | Stack 5-byte form of 1.
| E9  | STKONE    | Stack integer form of 1.
| EC  | STKTEN    | Stack 10.
| F0  | STKHALFPI | Stack PI/2

# Tape System

There are five types of tape files; Basic program, Machine Code, Numeric array, String array and SCREEN$. File saving occurs at a selectable speed which can be set to match Spectrum tape speeds. The header format is different from the Spectrum's and will not be recognised by a Spectrum as a header. The data block format is the same as on the Spectrum, but it may contain up to 512K. SCREEN$ files normally contain the palette settings (40 bytes) and line interrupt table, (1 to 509 bytes), so even a screen that switches the palette part-way down a screen can be reloaded. The screen mode is set appropriately before loading of the data block begins.

Files are loaded at the correct speed automatically. Spectrum CODE file headers are converted into the SAM equivalent and then used to load the data block. Spectrum CODE files can be loaded into the Coupé as either CODE or SCREEN$ files by specifying this after the LOAD command. (The Coupé distinguishes SCREEN$ files from CODE files because they have to be loaded to screen memory, which can be anywhere in the memory map). Coupé CODE files can be forced to load as SCREEN$ files, and vice versa, simply by using LOAD "name" CODE or SCREEN$. CODE files can have an execution address.

Altering the system variable TPROMPTS (SVAR 51) can turn off the prompt before SAVE, and/or the printing of file as names they are read from tape.

## File Header Format

Tape, disk and Net use a common header format as far as the Basic interpreter is concerned. (The DOS holds information in a slightly different format for its own use, but uses information from, and passes information to, the standard header buffers). SAVE uses a single buffer, HDR (Header-requested) at 4B00H where the details of the file to be
saved are built up before the header and then the data are saved. LOAD also uses this buffer, plus an extra one, HDL (Header-loaded) at 4850H which is used to load file headers for comparison with HDR (On the Coupé a "tape header reader" program just consists of a program to PEEK the HDL buffer). (NB There is an extra file type in SAMDOS - .SNP).

|    | |    |      |HEADER BUFFER FORMAT (HDR and HDL):
|----|-|----|------|-
|  0 | |    | (1)  | Type. 5 is a Spectrum 48K snapshot, 16 is a Basic program, 17 is a Numeric array, 18 is a String or string array, 19 is a CODE file, and 20 is a SCREEN$ file.
|  1 |-| 10 | (10) | File name, padded with spaces.
| 11 |-| 14 | (4)  | Allows longer file name if DEVICE is not T, for example 'D2:filenamexx'. SAMDOS will strip off any device identifier, so the maximum length of a filename is still ten characters.
| 15 | |    | (1)  | Flags. Bit 0 is set if the name is not to be printed on LOADing, bit 1 is set if the CODE is protected. The flags can be conveniently set during SAVE by: <br> SAVE CHR$ 1+"name" - sets bit 0 <br> SAVE CHR$ 2+"name" - sets bit 1 <br> SAVE CHR$ 3+"name" - sets both bits <br><br> (Characters <=3 as the first character in a file name just set the flags - they are not saved as part of the name). Flag bit 0 works in addition to the TPROMPTS system variable. Bit 1 protects CODE files; when this bit is set, an auto-running CODE file cannot be stopped by MERGE, or re-directed to another address by supplying one in, for example: LOAD start,length,newaddress.
| 16 |-| 26 | (11) | If type is 17 or 18, holds type/length byte and array name
| 16 | |    | (1)  | If type is 20, holds screen MODE.
| 16 |-| 18 | (3)  | If type is 16, holds program length excluding variables.
| 19 |-| 21 | (3)  | If type is 16, holds program length plus numeric variables.
| 22 |-| 24 | (3)  | If type is 16, holds program length plus numeric variables and gap length before string/array variables.
|    | |    |      | (The extra data for Basic programs allows NVARS, NUMEND and SAVARS to be set up on LOADing).
| 27 |-| 30 | (5)  | Reserved
| 31 | |    | (1)  | 16K page that file starts in (ignored on LOADing, except for CODE files). bits 4-0 hold the page, bits 7-5 are undefined. If type is 17 or 18 and the array being LOADed does not exist in memory, this byte in HDR will be FFH.
| 32 |-| 33 | (2)  | Offset within page of file start (ignored on LOADing, except for CODE files). The offset is 8000H-BFFFH, in LSB/MSB form.
| 34 | |    | (1)  | File length in 16K pages (in HDL, or HDR during SAVE) or requested start for CODE files in HDR during LOAD (FFH if there was no requested start). During LOAD of an array, "file length" in HDR is the length of the existing array in memory, or FFFFFF if there isn't one.
| 35 |-| 36 | (2)  | File length MOD 16K, plus 8000H (reset bit 15 of the length word to get the true length).
| 37 | |    | (1)  | If CODE file, page of execute address, or FF if there isn't one. If Basic program, 00 if there is an autorun line number in the next two bytes, or FF if there isn't one.
| 38 |-| 39 | (2)  | If CODE file, offset within page of execute address (8000-BFFFH, LSB/MSB) if there is one. If Basic program, auto-run line number if there is one.
| 40 |-| 79 | (40) | Comment field. Not initialised to anything, but SAVEd and LOADed with the program. Could be POKEd or PEEKed to carry extra information about the file. (DOS only SAVEs the first 8 bytes in this area).

# SAM BASIC

Numeric variable names must start with a letter. Numbers, letters, underlines and spaces may follow the first character, to a total of up to 32 characters (spaces do not count). (FOR-NEXT variables are treated like normal numeric variables).

String and array variable names are similar but limited to 10 characters (spaces do not count). String and string array names are followed by '$'. strings can be up to 65520 characters long. Arrays can fill all available memory, although no subscript can be over 64K. Program lines can have up to 127 statements, and can be up to 16127 bytes long.

Keywords are normally typed in full, although keys can be programmed to generate complete words. When a keyword is recognised, it is converted to capital letters in the listing A keyword which is followed by a letter will not be recognised, so printx is assumed to be a procedure name, but print x and print1 become PRINT x and PRINT 1.

If you press the EDIT key on its own, the line with '>' will appear in the editing area. If you type a line number and then press EDIT, the desired line will appear for editing. The cursor can be moved left, right, up or down in the edited line, using the cursor keys. The delete key deletes to the left; shift-delete deletes right.

# BASIC / Machine Code Interface

NB angle brackets enclose optional items.

``SAVE "name" CODE start,length<,execute address>``

Produces auto-running file if an execute address is used.

``LOAD "name" CODE <start><,length><,execute address>``

Executes file from execute address if used. Otherwise any execute address saved with the file is used. ``MERGE`` will stop a ``CODE`` file executing unless it is protected by setting a bit in the file header.

Start, length and execute values, and the addresses used by ``USR``, ``USR$``, ``CALL``, ``POKE``, ``PEEK`` etc. can be up to 528K minus 1.

``USR n``

Calls address n. Enters with BC=n. All registers can be used. USR returns the final value of BC.

``USR$ n``

As ``USR``, but returns a string BC bytes long starting at DE in page A. (Page is irrelevant if DE<8000H).

``CALL n``

Calls address n with a list of numeric or string parameters if desired. The values of numbers and the lengths and starts of strings are placed on the floating point calculator stack, with information on type. The A register contains the number of parameters when address n is entered. Using the FPC stack allows numbers to be removed and rounded to 2 bytes
with range checking by calling JGETINT in the jump table; floating-point numbers, or strings, can be unstacked using JSTKFETCH. strings shorter than 256 bytes can be copied to a buffer in the system variables area by calling JSBUFFET. (strings can be copied from anywhere in memory, even if they are paged out). JSTKSTORE can be used to place any result on the calculator stack.

``CLEAR n``

Set upper limit of Basic's RAM use.

``OPEN n``

Reserve n more 16K pages for Basic to use.

``OPEN TO n``

Allocate a total of n pages to Basic.

``CLOSE n``

Free n 16K pages.

``LENGTH``

This function returns the address and dimensions of arrays and strings, and the address of numbers. Useful for passing data via Basic's ``CALL``.

``POKE n,x``

POKE 1 byte

``POKE n,1,2,3``

POKE multiple bytes (up to 32)

``DPOKE n,x``

POKE 2 bytes (LSB/MSB)

``POKE n,a$``

POKE entire string

``PEEK n``

PEEK 1 byte

``DPEEK n``

PEEK 2 bytes

``MEM$(n TO m)``

PEEK a string, for example: ``LET a$=MEN$(70000 TO 71000)`` assigns 1000 bytes to a$ ``POKE 72000,a$`` puts those bytes to 72000.

MEM$ can read any RAM page (16K-528K-l) but will not read the ROM's. Use PEEK or DPEEK if you need to read ROM0.

Examples of base conversion:

BIN 1010=10
BIN$ 128="10000000"

HEX$ 74="4A"
HEX$ 16384="4000"
HEX$ 65539="010003"

&FF=255
&10003=65539

VAL("&"+a$)=255 if a$="ff"

# Major Pointers To BASIC's Memory Area

(ALL TAKE 3 BYTES, IN THE FORM: PAGE/OFFSET)

|        |                 |
|--------|-----------------
| PROC   | start of program
| NVARS  | start of numeric variables
| NUMEND | end of numeric variables gap (<=512 bytes)
| SAVARS | start of string/array variables
| ELINE  | start of edit line
| WORKSP | start of workspace
| WKEND  | end of workspace
|        | spare space
| RAMTOP | last byte allocated to basic program

See the section on system variables for full information.

## Page Allocation Table

The table at 5100H-5120H is very important; it holds a byte for every possible l6K RAM page in the Coupé, plus an FFH terminator byte. The first byte corresponds to the first 16K RAM page, the second to the second page, etc. Non-existent pages are also marked by FFH. Unused pages are marked as 00H. Pages used by the first Basic program in the machine are marked 40H; screen pages are marked C0H, and pages used by DOS (usually just one) are marked 60H.
On a 256K Coupé, the table (ALLOCT) will look like this after DOS has loaded:

40 40 40 40 00 00 00 00 00 00 00 00 00 60 C0 C0 FF FF FF etc.

A "Utilities" page is marked 20H. It is divided into 16 1K sections which can be used by assorted short utility programs. The final 16 bytes in a utilities page (SLOTT) show which 'slots" are reserved - a 0 shows the corresponding slot is free, and FFH that it is reserved. (The last slot is 16 bytes short of 1K). The proper method of allocating space for a short program is to look backwards through ALLOCT for 20H. If you find it switch in the indicated page and look backwards through SLOTT for a spare slot. Mark it and use that slot. (Or slots - you could reserve several slots). If you do not find a 20H entry in ALLOCT, look for 00H; report an error if none is found, else mark it 20H, clear the last 16 bytes of that page with zeros, and then reserve yourself some space in the new SLOTT you have just created.

Free pages can be used as temporary workspaces, provided you are sure that nothing is going to overwrite the page while you are using it. (Interrupts do not do this, but the DOS might).

## Keyboard

Any keyboard key in NORMAL, CAPS SHIFTED, SYM SHIFTED or CONTROL states can return any code (0-255). The 69 keys and 4 shift states give 276 key in a keyboard 'map'. This map has a seemingly haphazard arrangement that corresponds to the keyboard matrix see Appendix C for diagrams of the keyboard and the map positions, plus initial codes returned by each
position. E.g. map position 0 has 98 in it - so CHR$ 98 ('b') is produced when the actual key corresponding to that map position is pressed, without any shifts. The entire map can be altered if desired.

``KEY Posn,x``

``KEY 23,134`` makes key position 23 in the key map produce CHR$ 134 hen pressed.
``KEY 0,65`` would make the normal 'b' into CHR$ 65 ('A').
Posn must be 0-275, x must be 0-255.

When certain codes come from the keyboard, a search is made to see if an expanded definition has been made for them. Codes 192-254 can be defined in this way. If a definition does not exist, CHR$ 192-254 will be used, otherwise the expanded definition is used. This allows, for example, function keys to be defined as RUN (enter) or LIST (enter). See below.

``DEF KEYCODE``

``DEF KEYCODE 195: PRINT 123: PRINT "z"`` will cause any subsequent code of 195 corning from the keyboard to be expanded to: PRINT 123: PRINT "z"(ENTER). This makes: 123 z appear on the upper screen area. The entire line after DEF KEYCODE 195: is used. If a final colon is added to the line, the automatic (ENTER) is suppressed, for example:

``DEF KEYCODE 193: PRINT "asd":``
would produce:
``PRINT "asd"`` in the editing area.

DEF KEYCODE can also be used with a string, rather than the rest of a line, for example:

``DEF KEYCODE 192,"TESTING"`` will cause any subsequent code of 192 coming from the keyboard to be expanded to "TESTING" (ENTER). (This would cause an error report).
``DEF KEYCODE 192,"TESTING:"`` would suppress the (ENTER) because the
last character is a colon.

A particular definition can be cleared by:
``DEF KEYCODE 195:`` (followed by nothing)
 or ``DEF KEYCODE 195,""``
``DEF KEYCODE ERASE`` removes all definitions.

'Too many definitions' is reported if space runs out in the memory area used by DEF KEYCODE.

## Streams & Channels

``CLOSE``
``OPEN``

Like the Spectrum, streams 0 and 1 are normally OPEN to channel 'K'; PRINT #0;"test": PAUSE will print at the bottom of the screen. PRINT #2 will print on the upper part of the screen, as usual (using channel 'S'), and PRINT #3 acts like LPRINT (using channel 'P'). You can also do something like OPEN *#;"P": PRINT #6;"testing" to send data to the printer via stream 6, or OPEN #2;"P" so that the normal screen output goes to the printer instead. INPUT normally uses channel "K" (the lower screen), but INPUT#2 is allowed and uses the upper screen, (channel "S").

For example: INPUT #2;"Value:";v will allow you to type in the value of V on the upper screen, next to the 'Value:' prompt. The line is NOT cleared after you press enter, unlike the lower screen.

The RECORD command works via stream 16 (which did not exist on the Spectrum). Stream 16 prints to the string variable specified by RECORD, and it will still do so after RECORD STOP. This night be useful to some users: ~or example, RECORD TO a$: DIR #16;1 :RECORD STOP, will place a disk catalogue in a$. Other streams apart from 16 can be opened to the
string variable using, for example, OPEN #5;"$".

OPEN #s;"b" (or "B") will allow stream S to send anything to the printer - this is useful for sending control codes. (The problem with the 'p' stream is that control codes are acted on, and may not be sent to the printer - the TAB control code for example, will send a number of spaces to the printer). Channel 'p' actually uses channel 'b' for output, after it has modified the data it receives. Therefore all an advanced user need do to divert output to, say, a serial printer driver, is to alter the channel 'b' output address.

``SAVE``, ``LOAD``, ``MERGE``, ``VERIFY``

Allow programs, strings, arrays, machine code and screens images to be handled.

``SAVE "name" CODE start,length,execute-address`` is allowed, so that ``LOAD "name" CODE`` will start running from the address given. ``MERGE "name" CODE`` will suppress auto-running of code files.

``LOAD "name" DATA b$()`` works, but also, ``DATA addr$()`` or ``DATA abc$`` are allowed. Note that ``SAVE "name" DATA blit$`` is okay even if ``blit$`` is a simple string, such as a ``BLITZ`` string.

``LOAD "name" LINE n`` loads the program and goes to line number n. This overrides any auto-run line number saved with the program.

``SAVE "name" SCREEN$`` saves the screen image and the current mode and palette information for later reloading. (``LOAD`` automatically switches modes if required).

``DEVICE``

This new command makes SAVE, LOAD, MERGE and VERIFY work with the disk or Network.

``DEVICE d`` means use disk drive 1.
``DEVICE d1`` ditto
``DEVICE D1`` ditto
``DEVICE N5`` use Network station 5.
``DEVICE T`` use tape, SAVE speed similar to the spectrum's.
``DEVICE t35`` use tape, SAVE speed 35.
(Speed 112 is spectrum speed, 35 is much faster. Faster speeds are less reliable - but 3*spectrum speed should be feasible with many recorders. LOAD automatically adjusts to the tape speed that was used when the file was saved).

## Sound

``SOUND r,d``
``SOUND r,d;r,d;r,d...``

Sends data byte D to sound chip register R. Up to 127 pairs of numbers can be used.

This explanation is based on the program in the SAM Coupé User's Guide. The program is reproduced here for ease of reference

````
10 REM sound effects
20 GO SUB 3000

30 REM steam locomotive
40 LET L=7 : GO SUB 2000
50 LET p=20 : GO SUB 1000

100 REM flying saucer
110 LET L=3: GO SUB 2000
120 LET p=20 : GO SUB 1000

200 REM sonic scooter
210 SOUND 17,4 : SOUND 16,64
220 LET p=5 : GO SUB 1000 : PAUSE 200

300 REM telephone
310 GO SUB 3000
320 FOR n=0 TO 3
340 SOUND 2,255 : PAUSE 18
350 SOUND 2,0 : PAUSE 8
360 SOUND 2,255 : PAUSE 18
370 SOUND 2,0 : PAUSE 80
380 NEXT n 17,6,9,128,16,32,28,1

400 REM cuckoo
410 BEEP 0.2,19 BEEP 0,4,15
420 STOP

1000 REM stereo Left to Right
1010 LET a=0 : LET b=0
1020 LET L=1 : LET R=0 : GO SUB 1500
1030 LET L=0 : LET R=16 : GO SUB 1500
1040 LET L=-1 : LET R=0 : GO SUB 1500
1050 LET L=0 : LET R=-16 : GO SUB 1500
1060 RETURN

1500 REM output subroutine
1510 SOUND 2,(a+b) : PAUSE p
1520 FOR n=1 TO 15
1530 LET a=a+L : LET b=b+R
1540 SOUND 2,(a+b)
1550 PAUSE p : NEXT n
1560 RETURN

2000 REM output sound data
2010 DATA 9,64,16,16,17,0,24,138,28,1,21,4,20,0
2020 DATA 9,255,17,1,20,4
2030 DATA 24,142,20,4,10,111,
2040 FOR n=1 TO L
2050 READ a,d : SOUND a,d : NEXT n
2060 RETURN

3000 REM clear the sound
3010 FOR n=0 TO 31 : SOUND n,0 : NEXT n
3020 RETURN
````

Line 20 clears the sound chip's registers by setting them all to zero.

Line 40. L refers to the pairs of data on line 2010. The data pairs refer to setting up the various registers.

Line 50. p refers to the speed at which the sound is moved across the stereo field. If you play the sound demo program, you will find that the sonic scooter moves from left to right faster than either the steam locomotive or the flying saucer. The subroutine at line 1000 tells the computer where to place the sound across the stereo field. The subroutine at line 1500, outputs the sound on both left and right channels.

Both the flying saucer and sonic scooter are similar to the steam locomotive except that the steam locomotive uses white noise.

The sonic scooter changes the current octave, so that register 17's octave is 4 and register 16's octaves are set to 0 for generator 8, and 4 for generator 9. Notice also that the speed of movement of the scooter is faster than either the locomotive or the flying saucer.
The telephone is placed in the centre of the stereo field after clearing the sound chip again. This sound uses envelope register 24 and places a sound from tone register 10 through it using enable mixer 20 with bit 4 set. It also uses tone register 9 to control the speed of the envelope. Finally, register 28 enables the sound. The 'bleep' sound is controlled by switching the volume of amplitude register 2 between 0 and 255. This is repeated 4 times with pauses between each of the rings.

The cuckoo uses the BEEP command. This command, as on the Spectrum, does not use the sound chip at all, but the ASIC to generate the sound.

The subroutine at line 1000 sets up control data for the output subroutine at line 1500. Variables L and R set up which direction to go when 'ramping' the volume up or down on either channel, whist the subroutine at line 1500 does the ramping itself. Register 2 is the amplitude register which controls the sound. It is also here, on line 1550 that P is used to control the speed of the movement across the stereo field.

The subroutine at line 2000 holds the register data, and actually acts upon the data presented to the chip. Its function is to output any information to the various registers as it receives the data. The subroutine at line 3000 clears the sound chip by setting all registers to zero.

## Graphics Scaling System

XOS, XRG,
YOS, YRG

Control graphics scale and origin. XOS and YOS are offsets added to x and y coordinates when graphics commands are used. They allow the origin to be moved from the normal position just above the editing area, on the left. RUN or CLEAR resets XOS and YOS to zero; LET alters them. XRG and YRG alter the scale of the graphics system. XRG is normally 256, or 512 if 'thin' pixels are in use. YRG is normally 192. Altering XRG to, say, 1024 would make PLOT 950,100 a legal command by doing 256/1024*950 before plotting the pixel on the screen. (Altering the ranges by powers of 2 gives faster plotting).

Normally, modes 2 and 4, and mode 3 if 'fat' pixels are used, have a graphics coordinate system with 0,0 just above the bottom editing section, at the left, and 255, 173 at the top right.

If thin' pixels are in use, the normal X is expanded so that top right is 511,173. In mode 1, the default character height is 8 pixels, rather than 9, and 2 less scans are used by the editing area, so that the top of the screen is at a Y coordinate of 175.

The bottom 2 lines of the display can be plotted on using:
 PLOT 0,-10.
If the position of the origin is moved by LET XOS=-18 then 0,0 is at the very bottom left of the screen and 0,191 is the top left.

# Keyword Codes

The Coupé's functions are stored in the program as FFH (255) followed by 3BH-83H.

| Function | Dec | Hex
|----------|-----|-----
| PI       |  59 | 3B
| RND      |  60 | 3C
| POINT    |  61 | 3D
| FREE     |  62 | 3E
| LENGTH   |  63 | 3F
| ITEM     |  64 | 40
| ATTR     |  65 | 41
| FN       |  66 | 42
| BIN      |  67 | 43
| XMOUSE   |  68 | 44
| YMOUSE   |  69 | 45
| XPEN     |  70 | 46
| YPEN     |  71 | 47
| RAMTOP   |  72 | 48
| Reserved |  73 | 49
| INSTR    |  74 | 4A
| INKEY$   |  75 | 4B
| SCREEN$  |  76 | 4C
| MEM$     |  77 | 4D
| Reserved |  78 | 4E
| PATH$    |  79 | 4F
| STRING$  |  80 | 50
| Reserved |  81 | 51
| Reserved |  82 | 52
| SIN      |  83 | 53
| COS      |  84 | 54
| TAN      |  85 | 55
| ASN      |  86 | 56
| ACS      |  87 | 57
| ATN      |  88 | 58
| LN       |  89 | 59
| EXP      |  90 | 5A
| ABS      |  91 | 5B
| SGN      |  92 | 5C
| SQR      |  93 | 5D
| INT      |  94 | 5E
| USR      |  95 | 5F
| IN       |  96 | 60
| PEEK     |  97 | 61
| DPEEK    |  98 | 62
| DVAR     |  99 | 63
| SVAR     | 100 | 64
| BUTTON   | 101 | 65
| EOF      | 102 | 66
| PTR      | 103 | 67
| Reserved | 104 | 68
| UDG      | 105 | 69
| Reserved | 106 | 6A
| LEN      | 107 | 6B
| CODE     | 108 | 6C
| VAL$     | 109 | 6D
| VAL      | 110 | 6E
| TRUNC$   | 111 | 6F
| CHR$     | 112 | 70
| STR$     | 113 | 71
| BIN$     | 114 | 72
| HEX$     | 115 | 73
| USR$     | 116 | 74
| Reserved | 117 | 75
| NOT      | 118 | 76
| Reserved | 119 | 77
| Reserved | 120 | 78
| Reserved | 121 | 79
| MOD      | 122 | 7A
| DIV      | 123 | 7B
| BOR      | 124 | 7C
| Reserved | 125 | 7D
| BAND     | 126 | 7E
| OR       | 127 | 7F
| AND      | 128 | 80
| <>       | 129 | 81
| <=       | 130 | 82
| >=       | 131 | 83
| Reserved | 132 | 84

Codes from 85H to FEH do not need a preceding FFH; they are single-byte compressed forms of keywords. Context allows then to appear as keywords or as UDGs, as appropriate. For example, they will appear as keywords in a listing, unless inside quotes, but will appear as UDGs when PRINTed.

The tokens from 85H to 8FH are qualifiers - they have no result or action on their own, but simply modify the action at other commands. (This does not prevent an action routine being assigned to them. The DOS, for example, provides an action routine for WRITE).

| Token | Dec | Hex
|-------|-----|-----
| USING | 133 | 85
| WRITE | 134 | 86
| AT    | 135 | 87
| TAB   | 136 | 88
| OFF   | 137 | 89
| WHILE | 138 | 8A
| UNTIL | 139 | 8B
| LINE  | 140 | 8C
| THEN  | 141 | 8D
| TO    | 142 | 8E
| STEP  | 143 | 8F

The tokens from 90H-FFH are commands. The command address table (see System variables - CMDADDRT) contains a 2-byte address for each of them, starting with DIR. This is the address that handles the syntax checking and run-time action for the command.

| Command     | Dec | Hex
|-------------|-----|-----
| DIR         | 144 | 90
| FORMAT      | 145 | 91
| ERASE       | 146 | 92
| MOVE        | 147 | 93
| SAVE        | 148 | 94
| LOAD        | 149 | 95
| MERGE       | 150 | 96
| VERIFY      | 151 | 97
| OPEN        | 152 | 98
| CLOSE       | 153 | 99
| CIRCLE      | 154 | 9A
| PLOT        | 155 | 9B
| LET         | 156 | 9C
| BLITZ       | 157 | 9D
| BORDER      | 158 | 9E
| CLS         | 159 | 9F
| PALETTE     | 160 | A0
| PEN         | 161 | A1
| PAPER       | 162 | A2
| FLASH       | 163 | A3
| BRIGHT      | 164 | A4
| INVERSE     | 165 | A5
| OVER        | 166 | A6
| FATPIX      | 167 | A7
| CSIZE       | 168 | A8
| BLOCKS      | 169 | A9
| MODE        | 170 | AA
| GRAB        | 171 | AB
| PUT         | 172 | AC
| BEEP        | 173 | AD
| SOUND       | 174 | AE
| NEW         | 175 | AF
| RUN         | 176 | B0
| STOP        | 177 | B1
| CONTINUE    | 178 | B2
| CLEAR       | 179 | B3
| GO TO       | 180 | B4
| GO SUB      | 181 | B5
| RETURN      | 182 | B6
| REM         | 183 | B7
| READ        | 184 | B8
| DATA        | 185 | B9
| RESTORE     | 186 | BA
| PRINT       | 187 | BB
| LPRINT      | l88 | BC
| LIST        | 189 | BD
| LLIST       | 190 | BE
| DUMP        | 191 | BF
| FOR         | 192 | C0
| NEXT        | 193 | C1
| PAUSE       | 194 | C2
| DRAW        | 195 | C3
| DEFAULT     | 196 | C4
| DIM         | 197 | C5
| INPUT       | 198 | C6
| RANDOMIZE   | 199 | C7
| DEF FN      | 200 | C8
| DEF KEYCODE | 201 | C9
| DEF PROC    | 202 | CA
| END PROC    | 203 | CB
| RENUM       | 204 | CC
| DELETE      | 205 | CD
| REF         | 206 | CE
| COPY        | 207 | CF
| Reserved    | 208 | D0
| KEYIN       | 209 | D1
| LOCAL       | 210 | D2
| LOOP IF     | 211 | D3
| DO          | 212 | D4
| LOOP        | 213 | D5
| EXIT IF     | 214 | D6
| long IF     | 215 | D7
| short IF    | 216 | D8
| long ELSE   | 217 | D9
| short ELSE  | 218 | DA
| END IF      | 219 | DB
| KEY         | 220 | DC
| ON ERROR    | 221 | DD
| ON          | 222 | DE
| GET         | 223 | DF
| OUT         | 224 | E0
| POKE        | 225 | E1
| DPOKE       | 226 | E2
| RENAME      | 227 | E3
| CALL        | 228 | E4
| ROLL        | 229 | E5
| SCROLL      | 230 | E6
| SCREEN      | 231 | E7
| DISPLAY     | 232 | E8
| BOOT        | 233 | E9
| LABEL       | 234 | EA
| FILL        | 235 | EB
| WINDOW      | 236 | EC
| AUTO        | 237 | ED
| POP         | 238 | EE
| RECORD      | 239 | EF
| DEVICE      | 240 | F0
| PROTECT     | 241 | F1
| HIDE        | 242 | F2
| ZAP         | 243 | F3
| POW         | 244 | F4
| BOOM        | 245 | F5
| ZOOM        | 246 | F6
| Reserved    | 247 | F7
| Reserved    | 248 | F8
| Reserved    | 249 | F9
| Reserved    | 250 | FA
| Reserved    | 251 | FB
| Reserved    | 252 | FC
| Reserved    | 253 | FD
| Reserved    | 254 | FE
| Not usable <br> (function prefix) | 255 | FF

Certain new keywords will be implemented in a disk-based extended Basic, and these words should not be used in Basic programs as procedure or variable names, or subsequent editing of the program will be inconvenient (although ALTER is a search-and-replace, so you could
change every use of, for example, procedure SORT to SORTER, which would be okay). A provisional list of new keywords follows:

SORT, ALTER, USING$, SHIFT$, INARRAY, NUMBER, CHAR$, JOIN.

# SYSTEM VARIABLES

Note: The function SVAR N gives the result 5A00H+N.

|          | Hex  |     ||
|----------|------|-----|---------------
| LNCUR    | 5A00 |     | Cursor character for current line (usually '>').
| LCCUR    | 5A01 |     | Cursor character when caps lock is off (usually CHR$ 128).
| UCCUR    | 5A02 |     | Cursor character when caps lock is on (usually CHR$ 129).
| BIN1DIG  | 5A03 |     | Character used by BIN$ as "1" (usually "1").
| BIN0DIG  | 5A04 |     | Character used by BIN$ as "0" (usually "0").
| INSTHASH | 5A05 |     | Character used by INSTR as "match anything" character (usually CHR$ 35 "#"
| SLDEV    | 5A06 |     | Current device letter (usually "T" on a tape system, but can be "D", or "N").
| SELNUM   | 5A07 |     | Current tape save speed, or default drive number when a a disk drive is in use.
| SPEEDINK | 5A08 |     | Time between swaps of alternate PENs, in 50ths.of a second.
| LINIPTR  | 5A09 | (2) | Current position in line interupt palette change table.
| XCMDP    | 5A0B | (3) | Page/offset of first external command list, or FFxxxxH.
| PRRHS    | 5A0E |     | Printer right-hand column limit. (Usually 79, to give 80 columns; use 255 to give no limit)
| AFTERCR  | 5A0F |     | Character code sent to the printer after CHR$ 13 if channel "p" is in use. (Normally 10, to give automatic line teed. Use a value of 0 if no character is to be sent).
| LPTPRT1  | 5A10 | (2) | Printer control port/01H strobe value. The port is usually 233, with port 232 (one less) used for data. The second byte should always be 1.

The following system variables are only used when the screen dump utility has been loaded:

|        | Hex  |     ||
|--------|------|-----|--------------
| DMPLEN | 5A12 |     | Graphic dump length (in 8-pixel units; normally 22)
| DMPWID | 5A13 |     | Graphic dump width (in 8-fat pixel units; normally 32)
| DMPWM  | 5A14 |     | Graphic dump width multiplier (1 for normal width, 2 or 3 for double or triple width).
| DMPHM  | 5A15 |     | graphic dump height multiplier (1 for normal height, not 1 for double height).
| GCM1   | 5A17 |     | Initial message sent to printers before a dump. The first byte is the number of characters to send. The normal values are 6,27,108,8,27,51,24,0,0 (2 bytes are spare).
| GCM2   | 5A1F |     | Message sent to printers before each row is dumped. The first byte is the number of characters to send. The normal values are 5,13,10,27,42,4,0,0 (2 bytes are spare).
| GCM3   | 5A27 |     | Final message sent to printers after a dump. The first byte is the number of characters to send. The normal values are 4,13,10,27,64,0 (1 byte is spare).
| DMPTL  | 5A2D | (2) | Address in screen of top left corner for graphic dumps. (Usually 8000H).

(End of system variables used by dump utility).

|          | Hex  |     ||
|----------|------|-----|---------------
| TABVAR   | 5A2F |     | Zero for the print comma to tab by 16 columns (normal) or anything else for an 8-column tab.
| M23LSC   | 5A30 | (2) | Mode 3/4 lower screen colours. The first byte is PAPER*16+PAPER, the second is PEN*16+PEN, i.e. both nibbles in each byte match.
| SOFE     | 5A32 |     | Flag for screen off enable/disable. If it is zero (normal) the screen will go blank in modes 3 and 4 when the keyboard has not been used for 22 minutes. Use a 1 to disable.
| TPROMPTS | 5A33 |     | Bit 0=1 to suppress printing of file names during tape loading; bit 1=1 to suppress prompts during tape saving.

This is the start of a block of variables saved with a screen when it is no longer the current screen.

|        | Hex  |     ||
|--------|------|-----|--------------
| BGFLG  | 5A34 |     | Block graphics flag. Zero if BLOCKS 1, 1 if BLOCKS0.
| FL6OR8 | 5A35 |     | Zero if MODE 3 is using 6-pixel wide characters, otherwise non-zero.
| CSIZEH | 5A36 |     | Character height set by CSIZE command.
| CSIZEW | 5A37 |     | Character width set by CSIZE command.
| UWRHS  | 5A38 |     | Upper window right-hand column. starts at 31.
| UWLHS  | 5A39 |     | Upper window left-hand column. Starts at 0.
| UWTOP  | 5A3A |     | Upper window top row. starts at 0.
| UWBOT  | 5A3B |     | Upper window bottom row. starts at 18.
| LWRHS  | 5A3C |     | Lower window right-hand column. Starts at 31.
| LWLHS  | 5A3D |     | Lower window left-hand column. Starts at 0.
| LWTOP  | 5A3E |     | Lower window top row. Starts at 19.
| LWBOT  | 5A3F |     | Lower window bottom row. Starts at 20.
| MODE   | 5A40 |     | MODE of current screen. 0-3 for modes 1-4.
| YCOORD | 5A41 |     | Current graphics position y coordinate, with 0 at the top of the screen and 191 at the bottom.
| XCOORD | 5A42 | (2) | current graphics position x coordinate, with 0 at the left. The range is 0-255 unless "thin" pixels are in use (in which case the second byte is used and the range is 0-511).

The following are the "permanent" graphics/print variables, set by, for example, PEN 2, PAPER 4, OVER 1.

|         | Hex  ||
|---------|------|------------
| THFATP  | 5A44 | Zero if "thin" pixels in use, non-zero for "fat" pixels.
| ATTRP   | 5A45 | Attributes used by modes 1 and 2.
| MASKP   | 5A46 | Mask used by modes 1 and 2. Bits which are 1 make the corresponding attribute bit be taken from the screen, not ATTRP.
| PFLAGP  | 5A47 | Bit 4 is set for paper 9, bit 6 for pen 9
| M23PAPP | 5A48 | Mode 3/4 PAPER. Nibbles (mode 4) or double bits (mode 3) match unless striped paper is desired.
| M23INKP | 5A49 | Mode 3/4 PEN. Nibbles (mode 4) or double bits (mode 3) match unless a striped pen is desired.
| OVERP   | 5A4A | OVER status for printing. 0 for OVER 0, 1 for OVER 1 (XOR).
| INVERP  | 5A4B | 0 for INVERSE 0, 255 for INVERSE 1.
| GOVERP  | 5A4C | OVER status for graphics. 0-3 for normal, XOR, OR, AND.

Temporary graphics/print variables, set by, for example:
 PRINT PEN 3; PAPER 5;

They are temporary versions of the variables listed above.

|         | Hex  ||
|---------|------|-
| THFATT  | 5A4D | copied from thfatp when Mode=2, else set to not zero (fat)
| ATTRT   | 5A4E |
| MASKT   | 5A4F |
| PFLAGT  | 5A50 |
| M23PAPT | 5A51 |
| M23INKT | 5A52 |
| OVERT   | 5353 |
| INVERT  | 5A54 |
| GOVERT  | 5A55 |

Current window variables, copied from UWRHS etc. or LWRHS etc. according to which window is in use.

|         | Hex
|---------|------
| WINDRHS | 5A56
| WINDLRS | 5A57
| WINDTOP | 5A58
| WINDBOT | 5A59

The next three variables are at 5AB1H, 5B70H and 5B71H in version 1.0 ROMs.

|          | Hex  |     ||
|----------|------|-----|----------------------
| WINDMAX  | 5A5A | (2) | Upper window lowest bottom row/maximum right column. Used to limit the WINDOW command. Reset by the MODE command.
| ORGOFF   | 5A5C |     | Graphics origin offset from the screen bottom, in pixels.
| LSOFF    | 5A5D |     | Size of gap between upper and lower windows, in scan lines MOD CSIZEH.
| Reserved | 5A5E | (14)|
| SPOSNU   | 5A6C | (2) | Upper window position as column/row.
| SPOSNL   | 5A6E | (2) | Lower window position as column/row.

(End of block saved with a deselected screen).

|          | Hex  |     ||
|----------|------|-----|-------------
| PRPOSN   | 5A70 |     | Current printer column.
| Reserved | 5371 |     |
| OPCHAR   | 5A72 |     | Used by LPRINT - character being printed.
| DEVICE   | 5A73 |     | 0=upper window, 1=lower window, 2=printer, 3=other
| CLET     | 5A74 |     | Current channel letter K/S/P/B/T/$ etc.
| IFTYPE   | 5A75 |     | Long/short IF status.
| REFFLG   | 5A76 |     | Zero if a REF variable is being worked on.
| CURDISP  | 5A77 |     | Current display, set by the DISPLAY command.
| CUSCRNP  | 5A78 |     | Current screen page. Bit 7=0, bits 6 and 5=MODE (0-3) and bits 4-0=page number. Set by SCREEN command.
| CURP     | 5A79 |     | Current upper RAM port. (Temporary store during paging).
| CLRP     | 5A7A |     | Current lower RAM port. (Temporary store during paging).
| CSA      | 5A7B | (2) | Current statement address. Used by DOS.
| FIRST    | 5A7D | (2) |
| LAST     | 5A7F | (2) | Line numbers in, for example, LIST 20 TO 100.

The following variables point to the main sections of Basic's memory area. They are adjusted when space is made or reclaimed, as needed. In each set of three bytes, the first byte is the RAM page number (0-31) and the other two bytes are the offset in the page, plus 8000H. (In some circumstances the offset is allowed to be greater than 16K, but it is always less than 32K).

|          | Hex  |     ||
|----------|------|-----|---------------
| SAVARSP  | 5A81 |     |
| SAVARS   | 5A82 | (2) | String and array variables start
| NUMENDP  | 5A84 |     |
| NUMEND   | 5A85 | (2) | Numeric variables end
| NVARSP   | 5A87 |     |
| NVARS    | 5A88 | (2) | Numeric variables start
| DATADDP  | 5A8A |     |
| DATADD   | 5A8B | (2) | Data address used by READ command.
| WKENDP   | 5A8D |     |
| WKEND    | 5A8E | (2) | End of workspace. (Last used byte before RAMTOP).
| WORKSPP  | 5A90 |     |
| WORKSP   | 5A91 | (2) | workspace start.
| ELINEP   | 5A93 |     |
| ELINE    | 5A94 | (2) | Edit line start.
| CHADP    | 5A95 |     |
| CHAD     | 5A97 | (2) | Current character address.
| KCURP    | 5A99 |     |
| KCUR     | 5A9A | (2) | Address of cursor in the edit line.
| NXTLINEP | 5A9C |     |
| NXTLINE  | 5A9D | (2) | Address of next line in Basic program.
| PROGP    | 5A9F |     |
| PROG     | 5AA0 | (2) | Program start (address of line number of first line).
| XPTRP    | 5AA2 |     |
| XPTR     | 5AA3 | (2) | Address in the edit line of a syntax error.
| DESTP    | 5AA5 |     |
| DEST     | 5AA6 | (2) | Used in variable assignments.
| PRPTRP   | 5AA8 |     |
| PRPTR    | 5AA9 | (2) | Address of current procedure call.
| DPPTRP   | 5AAB |     |
| DPPTR    | 5AAC | (2) | Address of current DEF PROC statement.
| CLAPG    | 5AAE |     |
| CIA      | 5AAF | (2) | Address of start of current line.
| Reserved | 5AB1 |     |
| STRNO    | 5AB2 |     | Current stream number. used by DOS.
| LDCO     | 5AB3 |     | Offset when loading spectrum machine code (16K pages).
| Reserved | 5AB4 |     |
| OPSTORE  | 5AB5 | (2) | Temporary store for print output address.
| DMPFLG   | 5AB7 |     | If non-zero, printed characters are "thrown away".
| LISTFLG  | 5AB8 |     | 0/1/2 for LIST FORMAT 0/1/2.
| LSTFT    | 5AB9 |     | Temporary version of LISTFLG used by channel 'R'.
| INQUFG   | 5ABA |     | "In quotes" flag. Bit 0=1 if character being printed is inside quotes. LIST zeros this bit so initial state is "outside" and tokens are printed, except inside quotes. PRINT sets it to 1 so UDGs are printed instead of tokens.
| SPROMPT  | 5ABB |     | If non-Zero no "scroll?" prompts are given.

The next six variables are used by the indented listing routine.

|           | Hex  |     ||
|-----------|------|-----|---------------
| OLDSPCS   | 5ABC |     | Indent status of previous line.
| INDOPFG   | 5ABD |     | Flag.
| NXTSPCS   | 5ABE |     |
| CURSPCS   | 5ABF |     |
| NXTHSPCS  | 5AC0 |     |
| CURTHSPCS | 5AC1 |     |
| KPOS      | 5AC2 | (2) | Screen position of editing cursor.
| SOFFCT    | 5AC4 |     | Counter used by auto-screen off. Changes every 256 frames if the keyboard is not in use.
| SOFLG     | 5AC5 |     | Flag for screen has been turned off" (if nonzero).
| SPEEDIC   | 5AC6 |     | Counter for flashing inks.
| PALFLAG   | 5AC7 |     | Bit 0 shows which palette table in use, main or alternate.

Temporary stores:

|          | Hex  |     ||
|----------|------|-----|-
| TEMPW1   | 53C8 | (2) |
| TEMPW2   | 5ACA | (2) |
| TEMPW3   | 5ACC | (2) |
| TEMPB1   | 5ACE |     |
| TEMPB2   | 5ACF |     |
| TEMPB3   | 5AD0 |     |
| LASTSTAT | 5AD1 |     | Status port value on last interrupt.
| SPSTORE  | 5AD2 | (2) | stack pointer store used by maskable interrupts.
| JVSP     | 5AD5 | (2) | JSVIN stack pointer store.
| NMISP    | 5AD7 | (2) | Non-maskable interrupt stack pointer store.
| NMILRP   | 5AD9 | (1) | LMPR value when NMI occurred.

Vectors (see detailed description elsewhere).

|        | Hex  |     ||
|--------|------|-----|-----------
| DMPV   | 5ADA | (2) | Screen dump.
| SETIYV | 5ADC | (2) | Set IY register to pixel output routine.
| PRTOKV | 5ADE | (2) | Print a token.
| NMIV   | 5AE0 | (2) | Non-maskable interrupt.
| FRAMIV | 5AE2 | (2) | Frame interrupt.
| LINIV  | 5AE4 | (2) | Line interrupt.
| COMSV  | 5AE6 | (2) | Comms interrupt.
| MIPV   | 5AE8 | (2) | MIDI input interrupt.
| MOPV   | 5AEA | (2) | MIDI output interrupt.
| EDITV  | 5AEC | (2) | Editor.
| RST8V  | 5AEE | (2) | RST 08H (error handler).
| RST28V | 5AF0 | (2) | RST 28H (floating point calculator).
| RST30V | 5AF2 | (2) | RST 30H (user RST).
| CMDV   | 5AF4 | (2) | Command.
| EVALUV | 5AF6 | (2) | Expression evaluator.
| LPRTV  | 5AF8 | (2) | Printer.
| MTOFCV | 5AFA | (2) | Match token.
| MOUSV  | 5AFC | (2) | Mouse.
| KURV   | 5AFE | (2) | Edit cursor.

Tables used by MODE 3 and 4 to expand character pattern data (as stored in UDGs, for example), to a form suitable for placing on the screen. In MODE 3 each table holds 16 bytes (expanded versions of each possible nibble) while in MODE 4 each table holds 16 words (expanded versions of each nibble).

|          | Hex  |      ||
|----------|------|------|------------
| CEXTAB   | 5B00 | (32) | Coloured expansion table - current PEN, PAPER and INVERSE state are used to modify this data.
| EXTAB    | 5B20 | (32) | Uncoloured expansion table. E.g. in MODE 3 or 4, the nibble 1010b is expanded to 11001100b or 1111000011110000b.
| COMPFLG  | 5B40 |      | Flag bits used by LABEL/FN/PROC compiler.
| BREARDI  | 5B41 |      | Non-zero if ESC between statements is to be disabled.
| ERRSTAT  | 5B42 |      | Statement to go to ON ERROR.
| ERRLN    | 5B43 | (2)  | line to go to ON ERROR.
| ONERRFLG | 5B45 |      | Bit 7=temporary ON ERROR active flag, bit 0 is permanent.
| ONSTORE  | 5B46 |      | ON command's statement number.
| BCSTORE  | 5B47 | (2)  | Used by RST 30H to hold BC register.
| M3PAPP   | 5B49 | (2)  | used to bold MODE 4 PAPER and PEN when MODE 3 is used
| M3LSC    | 5B4B | (2)  | used to hold MODE 4 lower window colours when MODE 3 is in use.
| TEMPW4   | 5B4D | (2)  | Used by ADJUST POINTERS routine.
| TEMPW5   | 5B4F | (2)  | used by ADJUST POINTERS routine.
| Reserved | 5B51 |      |

Table used by the editor showing which screen lines have line numbers.

|          | Hex  |      ||
|----------|------|------|-
| LPT      | 5B52 | (30) |
| Reserved | 5B70 | (2)  |
| RNSTKE   | 5B72 | (2)  | Rename stack pointer used by procedures with REF.
| CURCHD   | 5B74 |      | Current Basic command.
| LTDFF    | 5B75 |      | LET/DEFAULT flag.
| STRMX6NN | 5B76 | (11) | Encoded type/length and name of the variable that stream 16 prints to. Set by RECORD TO command.
| GRARF    | 5B81 |      | Graphics record flag (0=off).
| DHADJ    | 5B82 |      | Double height adjust. Zero unless bottom of double-height character is being printed.
| PACCOUNT | 5B83 |      | Page counter used by FARLDIR and FARLDDR.
| MODCOUNT | 5B84 | (2)  | MOD 16K counter used by FARLDIR and FARLDDR.
| ECREG    | 5B86 | (2)  | calculator's BC register.
| AUTOFLO  | 5B88 |      | Zero if AUTO is off, else 1.
| AUTOSTEP | 5B89 | (2)  | AUTO command's step value.
| LSPTR    | 5B8E | (2)  | Line scan pointer used by the editor.
| LNPTR    | 5B8D | (1)  | Used by the editor.
| MSEDP    | 5B8E | (8)  | Used by the mouse as a data store.
| BUTSTAT  | 5B8F |      | Mouse button status.
| MXCRD    | 5B96 | (2)  | Mouse x coordinate.
| MYORD    | 5B98 | (2)  | Mouse y coordinate.

Used by the PRINT A NUMBER routine:

|          | Hex  |      ||
|----------|------|------|-
| FRACLIM  | 5B9A |      |
| NPRPOS   | 5B9B | (2)  |
| DIGITS   | 5B9D |      |
| EPOWER   | 5B9E |      |
| DECPNTED | 5B9F |      |
| PRNBUFF  | 5BA0 | (16) | ASCII form of number.
| BCDBUFF  | 5BB0 | (5)  |
| OTHER    | 5BB5 |      | Net destination station number.
| Reserved | 5BB6 |      |
| SLDEVT   | 5BB7 |      | Temporary device letter (usually copied from SLDEV).
| SLNUMT   | 5BB8 |      | Temporary device number (usually copied from SLNUM).
| OVERF    | 5BB9 |      | "SAVE OVER" flag used by DOS. Zero if SAVE OVER, else non-zero.
| INSLV    | 5BBA | (2)  | Block move vector.
| STRLOCN  | 5BBC | (2)  | Used by LOOK FOR A STRING/ARRAY VARIABLE routine.
| TVDATA   | 5BBE | (2)  | Used in handling control codes and their parameters.
| DOSER    | 5BC0 | (2)  | If address is non-zero, DOS jumps there on exit.
| DOSFLG   | 5BC2 |      | Zero if no DOS loaded, else page number containing DOS.
| DOSCNT   | 5BC3 |      | Bit 0 is set if DOS is in control of the system.
| BSTKEND  | 5BC4 | (2)  | End of Basic's stack (used by DO, GOSUB, procedures).
| BASSTK   | 5BC6 | (2)  | Start of Basic's stack.
| HEAPEND  | 5BC8 | (2)  | End of system heap.
| HPST     | 5BCA | (2)  | Start of system heap.
| FPSBOT   | 5BCC | (2)  | Start of floating point calculator stack.
| DKDEF    | 5BCE | (2)  | Start of KEYCODE definitions.
| DKLIM    | 5BD0 | (2)  | Limit address of KEYCODE buffer.
| PATOUT   | 5BD2 | (2)  | Address of 'printable characters' output routine.
| ERRMSGS  | 5BD4 | (2)  | Start of error message table.
| UMSGS    | 5BD6 | (2)  | Start of utility message table.
| KBTAB    | 5BD8 | (2)  | start of keyboard table.
| CMDADDRT | 5BDA | (2)  | Start of command address table.
| MNOP     | 5BDC | (2)  | Address of main output routine.
| MNIP     | 5BDE | (2)  | Address of main input routine.
| PAGER    | 5BE0 | (14) | Reserved for paging subroutine.
| KBUFF    | 5BEE | (18) | Keyboard scan table - 2 tables of 72 bits each.
| LEM1     | 5C00 |      | Used by keyscan
| LASTH    | 5C01 |      | Last key hit. Zero if no key. Stops changing if keys are not being read, when buffer fills. RES 5,(FLAGS) is seen as a read. Used by keyscan.
| KDATA    | 5C02 |      | Used by keyscan.
| LKPB     | 5C03 | (2)  |
| REPCT    | 5C05 |      | Used by keyscan.
| LASTKV   | 5C06 | (2)  | shift and key codes from last key press.
| KBHEAD   | 5C08 |      | Key from buffer queue head. Keeps last key value. Needs periodic resets of bit 5,(FLAGS) or buffer fills.
| REPDEL   | 5C09 |      | Delay before keys auto-repeat (in 50ths. of a second); normally 33.
| REPSPD   | 5C0A |      | Delay between key repeats (in 50ths. of a second); normally 3.
| Reserved | 5C0B |      |
| STREAMS  | 5C0C | (42) | For streams -5 to 15, a word gives the displacement from the start of the channels area to the assigned channel. If the word is zero, the stream is closed. Stream 16 is dealt with as stream -4.
| CHARS    | 5C36 | (2)  | Address 256 bytes below start of main character set.
| ERRSOUND | 5C38 |      | Length of error sound in 50ths. of a second; normally 60.
| CLICK    | 5C39 |      | Length of keyboard click (normally zero).
| ERRNR    | 5C3A |      | Error number.
| FLAGS    | 5C3B |      | Main flags byte.
| DFLAG    | 5C3C |      | Display flags.
| ERRSP    | 5C3D | (2)  | SP value to use when an error occurs.
| LISTSP   | 5C3F | (2)  | SP value to use when an automatic list fills the screen.
| Reserved | 5C41 |      |
| NEWPPC   | 5C42 | (2)  | New line to jump to.
| NSPPC    | 5C44 |      | New statement to jump to, or FFH.
| PPC      | 5C45 | (2)  | Current line number during program execution.
| SUBPPC   | 5C47 |      | Current statement number.
| BORDCR   | 5C48 |      | Attributes for lower screen in MODEs 1 and 2.
| EPPC     | 5C49 | (2)  | Number of line with > cursor.
| BORDCOL  | 5C4B |      | Value to send to border port.
| CHANS    | 5C4F | (2)  | start of channels area.
| CURCHL   | 5C51 | (2)  | start of current channel.
| DEFADDP  | 5C53 |      | DEF FN address (page).
| DEFADD   | 5C54 | (2)  | DEF FN address (offset)
| Reserved | 5C56 | (15) |
| STKEND   | SC65 | (2)  | End of floating point calculator stack.
| KPFLG    | 5C67 |      | Function keys if even, number pad if odd.
| MEN      | 5C68 | (2)  | Start of calculator's memory area.
| KLFLAG   | SC6A |      | 8 if caps lock is on, else zero.
| SDTOP    | 5C6C |      | Line number of top line in an automatic listing.
| COPPC    | 5C6E |      | Line number that CONTINTUE goes to.
| COSPPC   | 5C70 |      | statement number that CONTINUE goes to.
| FLAGE    | 5C71 |      | Flags used by INPUT command and the editor.
| STRIL    | 5C72 |      | Used when variables are assigned to.
| SEED     | 5C76 |      | Random number seed. Set by RANDOMIZE.
| FRAMES   | 5C78 | (3)  | Frames since machine was switched on (LSB first).
| UDG      | SC7B | (2)  | Address of CHR$ 144.
| HUDG     | SC7D | (2)  | Address of CHR$ 169 (initially undefined).
| FRAMES34 | 5C7F | (2)  | 2 more bytes of FRAMES counter.
| OLDPOS   | 5C82 |      | Used by editor in clearing lower window.
| SCRCT    | 5C8C |      | Counter used to give "scroll?" prompt.
| KBQB     | 5C8D | (8)  | Keyboard queue. At 5A5AH in vl.0 ROM.
| KBQP     | 5C95 | (2)  | Keyboard queue end/head pointers. At 5A6AH in vl.O ROM.
| Reserved | 5C97 | (6)  |
| SCPTR    | 5C9D | (2)  | Address in SCLIST at current screen's entry.
| FISCRNP  | 5C9F |      | Page of screen 1.
| SCLIST   | 5CA0 | (16) | Screens list. MODE/page of screens 1-16, or FFH if screen is closed. Bits 6 and 5=MODE, 4-0=page.
| LASTPAGE | 5CB0 |      | last page reserved by Basic. set by OPEN, OPEN TO or CLOSE.
| RAMTOPP  | 5CB1 |      | Page of RAMTOP.
| RAMTOP   | 5CB2 | (2)  | Offset of RAMTOP.
| PRAMTP   | 5CB4 |      | Last 16K page physically present in machine.

# Variable Formats

The Coupé has five main variable types:
- Numeric variables
- FOR-NEXT variables
- Strings
- String arrays
- Numeric arrays

Numeric variables and FOR-NEXT variables are kept in the area pointed to by NVARS and NVARSP. This area begins with 26 2-byte entries, which hold the offset to the first variable starting with a given letter (from A-Z - hence 26 entries). If the offset is FFFFH, there are no variables starting with this letter. For each numeric variable, the start of the variable has this form:

Type/name length byte, offset LSB, MSB, character1, character2...

The type/length byte stores the name length-1 in bits 4-0 (so names can be up to 32 characters long). Bit 5 is set if the variable is no longer in use, bit 6 is set for a FOR-NEXT variable and bit 7 is set if the variable is "hidden" (this is used by procedures to implement LOCAL variables). The offset is the distance to move from the MSB of the current offset to the type/length byte of the next variable starting with the same letter, or FFFFH if there are no more such variables. There may be from zero to 31 characters after the offset, forced to lower case if they are letters, and excluding spaces.

After this come five bytes to hold the value of the variable. (See the section on the floating point calculator for information on the makeup of these 5 bytes). If it is an ordinary numeric variable, there is just a value, but a FOR-NEXT variable has an additional 14 bytes; the complete format is:

VALUE (5): LIMIT (5): STEP (5): LOOP ADDRESS (3): STATEMENT (1)

The loop address is the page and offset (8000-BFFFH) of the start of the line to loop back to, and the statement is the number of the statement within that line to loop back to (loops to the first statement are thus the fastest).

Strings and arrays are kept in the area pointed to by SAVARS and SAVARSP. There is a buffer zone between the numeric and string/array variables, so that creation of a new numeric variable does not usually require the strings and arrays to be moved.

Variables in this area are in the order of their creation (by DIM or LET; LET a$=a$ will move a$ to the end of the area, unless a$ is an array). For each variable, the format is as follows:

Type/length byte, character1....character10, length (3)

The type/length byte holds the name length (1-10) in bits 4-0. Bit 6 is set for string arrays, bit 5 is set for numeric arrays, and both bits are reset for ordinary strings. Bit 7 is set if the variable is "hidden". Ten bytes of space follow to hold the variable name; unused bytes are undefined. The length is given as number of 16K pages, then length MOD 16K (LSB/MSB), for the rest of the array plus the 3 length bytes. For strings, the text of the string follows; for arrays, the next byte is the number of dimensions, followed by the length of dimension 1, dimension 2, etc. (2 bytes for each dimension). The array data then follows, all data with a first subscript of 1 being first, then the data with a first subscript of 2, etc. FFH terminates the list of string and array variables.

## Format Of A Basic Program

The first line of a program is pointed to by PROG and PROGP (offset 8000-BFFFH and page). Each line has the format:

LINE NUMBER (MSB/LSB): LINE LENGTH (LSB/MSB): TEXT: 0DH

Note that the line number is unusual in being stored most significant byte first. The line length is the length of the text and 0DH terminator. The line text contains compressed keywords (see keyword code table) and invisible forms of all literal numbers (decimal, binary and hexadecimal). The invisible forms are 0EH followed by 5 bytes to store the value. The line may also contain control codes and their parameters.

The final line in the program is followed by FFH (so the maximum line number allowed is FEFFH).

# SAM Coupé Disk Operating System

# Introduction

SAMDOS has been designed specifically for the SAM Coupé computer. It is similar to G+DOS as used with the MGT Plus D spectrum disk interface.

## Disk Drive

The internal SAM disk drive is a Citizen 3.5" slimline drive. Each drive is cased and fitted with the MGT disk controller interface, which utilises a VL-1772-02 floppy disk controller. By default the disks are formatted as double sided, 80 track per side, 10 sectors per track, to the IBM 3740 standard.

## Disk Format

We use 80 tracks per side, giving 160 tracks per disk. A track is made up of 10 data sectors, each giving 512 bytes of storage. The first 4 tracks of the disk are given up to the SAMDOS directory, leaving 156 tracks available for storage. This leaves available 1560 data sectors of 512 bytes (798720 bytes)

Although each data sector can hold 512 bytes, only 510 bytes of them are available for storage. The last two bytes of the data sector are used by the DOS to locate the next part of the file stored. Byte 511 holds the next track used by the file, while byte 512 holds the next sector.

# Disk File Header

At the beginning of each disk file there is a file header. The file header is 9 bytes long:

|     | SAMDOS type   | Plus D type
|-----|---------------|------------
| 0   | File type     | File type
| 1-2 | Modulo length | Length of file
| 3-4 | Offset Start  | Start Address
| 5-6 | Unused
| 7   | Number of pages
| 8   | Starting page number

Details of the Plus D header can be found in the technical information for the Plus D.

## File Type

Each file type in the SAMOOS is allocated a numeric identifier:

|    |                   |        |
|----|-------------------|---------
|  5 | ZX Snapshot file  | SNP 48k
| 16 | SAM BASIC program | BAS
| 17 | Numeric array     | D ARRAY
| 18 | String array      | $ ARRAY
| 19 | Code file         | C
| 20 | Screen file       | SCREEN$

## Modulo Length & Number Of Pages

In the SAMDOS header the length of the file is calculated by multiplying
the number of pages (byte 7) by 16384 and adding the modulo length (word
1-2), LSB/MSE, i.e. the length MOD 16K.

## Offset Start & Starting Page Number

Read starting page number (byte 8): AND this with 1FH to get the page number in the range 0 to 31. To find the start multiply the page number by 16384, add the offset, and subtract 4000H (since the ROM occupies 0-
3FFFH).

When SAMDOS is paged in it resides at 4000H, and ROM0 is placed at 0-3FFFH.

## SAMDOS Directory

The first 4 tracks of the disk are allocated to the disk directory, starting at track 0, sector 1. These 4 tracks give us 40 sectors each split into two 256 bytes entries. Each of these entries will identify one file, thus allowing up to 80 entries in the directory.

The format of each directory entry is as follows:

(The User Information File Area CUIFA) will be described later).

| Byte    | UIFA  | Description
|---------|-------|------------
| 0       | 0     | STATUS/FILE TYPE. <br> This byte is allocated one of the file types listed previously, but is also used as a file status. If the byte is 0 then the file has been erased. If the file is HIDDEN then bit 7 is set. If the file is PROTECTED then bit 6 is set.
| 1-10    | 1-10  | FILENAME. <br> This filename can be up to 10 characters
| 11      |       | MSB OF THE NUMBER OF SECTORS USED IN THE FILE.
| 12      |       | LSB OF THE NUMBER OF SECTORS USED IN THE FILE.
| 13      |       | TRACK NUMBER FOR START OF FILE
| 14      |       | SECTOR NUMBER FOR START OF FILE
| 15-209  |       | SECTOR ADDRESS MAP (195 BYTES) <br> (detailed further on).
| 210-219 |       | MGT FUTURE AND PAST (10 BYTES) <br> These were used in the PLUS D directory but are not used by the SAMDOS. They are allocated to MGT for future use.
| 220     | 15    | FLAGS (MGT USE ONLY)
| 221-231 |       | FILE TYPE INFORMATION
|         | 16-26 | If the file type is 17 or 18 then these bytes contain the file type/length and name.
|         | 16    | If the file type is 20 then these bytes contain the screen mode.
|         | 16-18 | If the file type is 16 then these bytes contain the program length excluding variables.
|         | 19-21 | If the file type is 16 then these bytes contain the program length plus numeric variables.
|         | 22-24 | If the file type is 16 then these bytes contain the program length plus numeric variables and the gap length before string and array variables.
| 232-235 | 27-30 | SPARE 4 BYTES (reserved).
| 236     | 31    | START PAGE NUMBER, in bits 4-0, bits 7-5 are undefined.
| 237-238 | 32-33 | PAGE OFFSET (8000-BFFFH). This is as per file header, although when the ROM passes a file to be saved it starts it in section C of the addressing map.
| 239     | 34    | NUMBER OF PAGES IN LENGTH. (as per file header)
| 240-241 | 35-36 | MODULO 0 TO 16383 LENGTH, i.e. length of file MOD 16384. (as per file header)
| 242-244 | 37-39 | EXECUTION ADDRESS <br> Execution Address, if CODE file, or line number if an auto-running BASIC program.
| 245-253 | 40-47 | SPARE 8 BYTES
| 254-255 |       | FOR FUTURE USE BY MGT ONLY.

## Sector Address Map

SAMDOS allocates 195 bytes to the sector address map, giving 1560 bits, which is the exact number of sectors available for storage on the drive.

A sector address map is calculated for each directory entry. when a file is created a directory entry is made for that file. A sector address map is created by setting the specific bit(s) corresponding to the sector(s) allocated to the file. (Bit 0 of the first byte is allocated to track 4 sector 1). For example, if the file uses 5 sectors then five corresponding bits in the sector address map are set and saved as part of the directory entry.

## Bit Address Map (BAM)

The bit address map is not stored on the disk by SAMDOS. It is generated by performing a bitwise OR of each file's sector address map. This then gives SAMDOS a usage map of the disk. When a file is created the first thing SAMDOS does is calculate the BAM, and then by looking at the available sectors (i.e. bits not set), it can work out if there is room for the file. If there is room for the file, then the directory entry is created, including the sector address map specific to the new file, and the file is stored in the sectors which have been specified in the file's sector address map.

# SAMDOS Interfacing

SAMDOS's machine code interface provides pointers to specific parts of the DOS, called hook codes. These pointers perform the DOS functions, e.g., SAVE, LOAD, VERIFY, etc.

To use these hook codes various registers in the Z80B must be set up for the subroutine called to perform the required tasks. Each hook code is described later in this manual together with the necessary register information.

When a hook code is used the ROM will page SAMDOS temporarily into section B of the 64K addressing space (ie at 400011):

````
rst 8   ; call ROM RST 8
defb x  ; Where x equals the specific Hook code required.
````

If an error occurs it will normally be handled by the ROM, producing an error message in the lower part of the screen. However, if the system variable DOSER (5BC0H) is loaded with the address of your own 'return from DOS' routine then this routine will be entered after SAMDOS has executed any hook codes, or examined any of BASIC's error codes, with the Accumulator holding zero for no error, or an error number. This will be either one of BASIC's error codes or a SAMDOS error code of 128 and above.

## User Information File Area (UIFA)

When using SAMDOS hook codes the calling program must set up an area in memory, pointed to by the IX register, which details the information required for file handling, e.g., SAVE and LOAD. This file is called the UIFA.

| Byte  | Description
|-------|------------
| 0     | STATUS/FILE TYPE.
| 1-14  | FILENAME. 14 characters are allocated to allow for device identification, for example: D1:filenamexx. SAMDOS will strip off the device identifier, so the maximum length of a filename is still ten characters.
| 15    | FLAGS
| 16-26 | If the file type is 17 or 18 then these bytes contain the type/length byte and the name.
| 16    | If the file type is 20 then this byte contains the screen mode.
| 16-18 | If the file type is 16 then these bytes contain the program length excluding variables.
| 19-21 | If the file type is 16 then these bytes contain the program length plus the numeric variables.
| 22-24 | If the file type is 16 then these bytes contain the program length plus the numeric variables and the gap length before the character variables.
| 27-30 | SPARE 4 BYTES (Reserved)
| 31    | 16K PAGE NUMBER START
| 32-33 | PAGE OFFSET (8000-BFFFH) LSB/MSB
| 34    | NUMBER OF PAGES IN LENGTH
| 35-36 | MODULO 0 TO 16383 LENGTH ie file length MOD 16384.
| 37    | EXECUTE PAGE NUMBER if applicable
| 38-39 | EXECUTE OFFSET (8000-BFFFH) LSB/MSB if applicable
| 40-47 | SPARE 8 BYTES (Comment Field)

When the DOS has used the UIFA and it wants to pass a UIFA back, eq, for confirmation of load by the calling program the DOS creates a Disk Information File Area (DIFA). Both the UIFA and DIFA are 48 bytes long. This confirmation DIFA is written to an area of memory 80 bytes above the user's specified UIFA.

## SAMDOS Hook Codes

SAMDOS provides the user with hook (command) codes which enable the machine code programmer to use SAMDOS's facilities without having to return to or call SAM BASIC.

If an error occurs, SAMDOS set the Carry flag and put an error number into the Accumulator. If no error occurs the Accumulator will equal zero.

The Hook Codes currently available are:

|       | Hex | Dec ||
|-------|-----|-----|----------
| INIT  | 80  | 128 | Initialise and look for AUTO file
| HGTHD | 81  | 129 | Get file header
| HLOAD | 82  | 130 | Load file
| HVERY | 83  | 131 | Verify file
| HSAVE | 84  | 132 | Save file
| HVAR  | 8B  | 139 | Get address of DVAR
| HOFLE | 93  | 147 | Open a File
| SBYT  | 94  | 148 | Save a byte
| HWSAD | 95  | 149 | Write a sector to the disk
| HSVBK | 96  | 150 | Save a block of data
| CFSM  | 98  | 152 | Close file sector map
| HGFLE | 9E  | 158 | Get a file from disk
| LBYT  | 9F  | 159 | Load a byte
| HRSAD | A0  | 160 | Read a sector from the disk
| HLDBK | A1  | 161 | Load a block of data from disk
| REST  | A4  | 164 | Restore disk drive to track 0
| PCAT  | A5  | 165 | Perform a directory listing
| HERAZ | A6  | 166 | Erase a file from disk

Provision has been made for further hook codes to be added to SAMDOS.

HOOK CODE EXPLANATIONS

When the hook code explanation refers to 'RPT', it refers to the pointer used internally by SAMDOS.

|       ||
|-------|-------
| INIT  | This routine looks for an AUTO file on the current disk, and initialises the DVARS.
| HGTHD | Get file header. This routine should be called with IX pointing to the UIFA, which should contain the file type and filename required. When completed the complete file header will be transferred in DIFA form to IX+80 bytes.
| HLOAD | Load file in UIFA pointed to by IX register. The C register contains the number of 16K pages used by the file, while DE must contain the length modulo 16K. The HL register pair must point to a destination between 8000H to BFFFH, while the destination page must be paged in using the HMPR register. These values can be obtained from the header loaded by HGTHD.
| HVERY | Verify the memory to the file stored on the disk. Again the IX register must be a pointer to the file UIFA. Use as HLOAD, but verifies rather than loads.
| HSAVE | Save the file whose UIFA is pointed to by the IX register. The UIFA must be a complete UIFA, including file length, etc.
| HVAR  | This routine calls the jump table thus unstacking the number following the DVAR into BC. The routine supplies the address of the DVAR by putting it onto the BASIC floating point calculator stack.
| HOFLE | Open a file on the disk. ix roust point to the UIFA. The routine will create a sector address map, and save the header to the disk and reset pointer RPT.
| SBYT  | Save the byte in the Accumulator to the RAM pointed to by the pointer RPT. If the sector is full the data will be stored in the next sector pointed to by the sector address map.
| HWSAD | D contains the track number, and E contains the sector number. The Accumulator holds the drive number (1 or 2). Writes the sector pointed to by the DE register pair. The Accumulator contains the drive number, while the HL register pair is the pointer to the source data which must be resident in the 64K address map.
| HSVBK | Save a block of data to the disk where the DE register pair points to the start of the data, and the BC register pair holds the byte count.
| CFSM  | Close file sector map. This routine empties the RAM and copies the header area on to the directory, closes the file, then updates the directory.
| HGFLE | Get a file from the disk. The IX register must point to the UIFA. The return is made with the first sector of the file loaded into RAM and RPT pointing to the first byte.
| LBYT  | Load the byte pointed to by RPT from RAM, place it in the Accumulator, and increment the RPT. When the sector has all been read then the next sector is loaded from the disk and the pointer adjusted.
| HRSAD | D contains the track number, and E contains the sector number. The Accumulator holds the drive number (1 or 2). Reads the sector pointed to by the DE register pair. The Accumulator contains the drive number, while the HL register pair is the pointer to the destination.
| HLDBK | Load a block of data from the disk to the memory pointed to by DE with the block count in BC.
| REST  | Restore disk drive to track 0. The Accumulator holds the drive number , ie, 1 or 2.
| PCAT  | Perform a directory listing to current stream.
| HERAZ | Erase a file from the disk. Register IX must point to the UIFA of the file to be erased.

## Locating SAMDOS

When SAMDOS is loaded the ROM looks at its available memory and loads SAMDOS into the last free 16K page. The ROM uses the last two 16K pages for SCREEN 1, so SAMDOS usually loads into the third from last 16K page, but the page will be different if extra screens have been opened before SAMDOS is loaded. Address 5BC2H (SVAR 450) holds the page number used by SAMDOS, or zero if SAMDOS has not been loaded.

``PEEK SVAR 450*16384+16384`` will give the start address of SAMDOS, When a DOS command is issued the DOS is loaded into section B (4000H) of the 64k addressing space, the command is performed, and the DOS is then paged out.

## SAMDOS Error codes

81. Nonsense in SAMDOS
82. Nonsense in SNOS (SAM Network operating system)
83. statement end error
84. Escape requested
85. TRK nnn SCT nnn error
86. Format TRK nnn lost
87. Check disk in drive
88. No BOOT file
89. Invalid file name
90. Invalid Station
91. Invalid device
92. variable not found
93. verify failed
94. Wrong file type
95. Merge error
96. Code error
97. Pupil set
98. Invalid code
99. Reading a write file
100. writing a read file
101. No AUTO file
102. Network off
103. No such drive
104. Disk is write protected
105. Not enough space
106. Directory full
107. File not found
108. End of file
109. file name used
110. No SAMDOS loaded
111. Stream used
112. Channel used

# Stop Press

## New System Variable (ROM 1.2)

|      |       ||
|------|-------|-
| 5B70 | ANYIV | This address is jumped to when *any* interrupt occurs. Normally ANYIV contains the address of the ROM's interrupt handler (0049H). On entry to the address stored in ANYIV, the B register holds the LMPR state when the interrupt occurred, the C register holds the status port state 6-9 microseconds after the interrupt occured. The AF, BC and HL register pairs have been stacked with the values they had when the interrupt occured. The system variables (page 0) is paged in at 4000H. (This may have switched out the stack!) HL holds the contents of ANYIV. Your code will be entered 19-23 microseconds after the interrupt signal occured. <br><br> For example: <br><br> ``ld a,b`` <br> ``out (lmpr),a`` <br> ``pop hl`` <br> ``pop bc`` <br> ``pop af`` <br> ``ei`` <br> ``ret`` <br><br> No keyscan or other interrupt events will happen. Alternatively, JP back to 0049H (the ROM's interrupt handler), with the B register unchanged.
